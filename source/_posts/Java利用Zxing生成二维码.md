---
title: Java利用Zxing生成二维码
date: 2018-2-12 22:42:37
tags: [Java,Code]
categories:
  - Java
---
#### Maven 依赖
```
<dependency>   
    <groupId>com.google.zxing</groupId>   
    <artifactId>core</artifactId>   
    <version>2.0</version>   
</dependency>  
```
#### 二维码的生成
* 利用Maven将Zxing-core.jar 包加入到项目中。
* 二维码的生成需要借助MatrixToImageWriter类，该类是由Google提供的，可以将该类拷贝到源码中，这里我将该类的源码贴上，可以直接使用。

```java
import com.google.zxing.common.BitMatrix;   
import javax.imageio.ImageIO;   
import java.io.File;   
import java.io.OutputStream;   
import java.io.IOException;   
import java.awt.image.BufferedImage;   
   
   
public final class MatrixToImageWriter {   
   
private static final int BLACK = 0xFF000000;   
private static final int WHITE = 0xFFFFFFFF;   
   
private MatrixToImageWriter() {}   
   
   
public static BufferedImage toBufferedImage(BitMatrix matrix) {   
    int width = matrix.getWidth();   
    int height = matrix.getHeight();   
    BufferedImage image = new BufferedImage(width, height, BufferedImage.TYPE\_INT\_RGB);   
    for (int x = 0; x < width; x++) {   
        for (int y = 0; y < height; y++) {   
            image.setRGB(x, y, matrix.get(x, y) ? BLACK : WHITE);   
        }   
    }   
    return image;   
}   
   
   
public static void writeToFile(BitMatrix matrix, String format, File file) throws IOException {   
    BufferedImage image = toBufferedImage(matrix);   
    if (!ImageIO.write(image, format, file)) {   
        throw new IOException("Could not write an image of format " + format + " to " + file);   
    }   
}   
   
   
public static void writeToStream(BitMatrix matrix, String format, OutputStream stream) throws IOException {   
    BufferedImage image = toBufferedImage(matrix);   
    if (!ImageIO.write(image, format, stream)) {   
        throw new IOException("Could not write an image of format " + format);   
    }   
}   
   
}  
```

#### 编写生成二维码的实现代码

```java
try {   
   
    String content = "http://www.baidu.com";   
    String path = "C:/Users/Administrator/Desktop/testImage";   
       
    MultiFormatWriter multiFormatWriter = new MultiFormatWriter();   
       
    Map hints = new HashMap();   
    hints.put(EncodeHintType.CHARACTER\_SET, "UTF-8");   
    BitMatrix bitMatrix = multiFormatWriter.encode(content, BarcodeFormat.QR\_CODE, 400, 400,hints);   
    File file1 = new File(path,"测试打开百度.jpg");   
    MatrixToImageWriter.writeToFile(bitMatrix, "jpg", file1);   
   
} catch (Exception e) {   
    e.printStackTrace();   
}  
```

现在运行后即可生成一张二维码图片

#### 二维码的解析

* 利用Maven将Zxing-core.jar 包加入到项目中。
* 和生成一样，我们需要一个辅助类（ BufferedImageLuminanceSource），同样该类Google也提供了，这里我同样将该类的源码贴出来，可以直接拷贝使用个，省去查找的麻烦 

```java 
import com.google.zxing.LuminanceSource;   
   
import java.awt.Graphics2D;   
import java.awt.geom.AffineTransform;   
import java.awt.image.BufferedImage;   
   
public final class BufferedImageLuminanceSource extends LuminanceSource {   
   
    private final BufferedImage image;   
    private final int left;   
    private final int top;   
       
    public BufferedImageLuminanceSource(BufferedImage image) {   
        this(image, 0, 0, image.getWidth(), image.getHeight());   
    }   
       
    public BufferedImageLuminanceSource(BufferedImage image, int left, int top, int width, int height) {   
        super(width, height);   
        int sourceWidth = image.getWidth();   
        int sourceHeight = image.getHeight();   
        if (left + width > sourceWidth || top + height > sourceHeight){   
            throw new IllegalArgumentException("Crop rectangle does not fit within image data.");   
        }     
        for (int y = top; y < top + height; y++) {   
            for (int x = left; x < left + width; x++) {   
                if ((image.getRGB(x, y) & 0xFF000000) == 0) {   
                    image.setRGB(x, y, 0xFFFFFFFF); // = white   
                }   
            }   
        }   
           
        this.image = new BufferedImage(sourceWidth, sourceHeight, BufferedImage.TYPE\_BYTE\_GRAY);   
        this.image.getGraphics().drawImage(image, 0, 0, null);   
        this.left = left;   
        this.top = top;   
    }   
       
    @Override   
    public byte[] getRow(int y, byte[] row) {   
        if (y < 0 || y >= getHeight()) {   
            throw new IllegalArgumentException("Requested row is outside the image: " + y);   
        }   
        int width = getWidth();   
        if (row == null || row.length < width) {   
            row = new byte[width];   
        }   
        image.getRaster().getDataElements(left, top + y, width, 1, row);   
        return row;   
    }   
       
    @Override   
    public byte[] getMatrix() {   
        int width = getWidth();   
        int height = getHeight();   
        int area = width * height;   
        byte[] matrix = new byte[area];   
        image.getRaster().getDataElements(left, top, width, height, matrix);   
        return matrix;   
    }   
       
    @Override   
    public boolean isCropSupported() {   
        return true;   
    }   
       
    @Override   
    public LuminanceSource crop(int left, int top, int width, int height) {   
        return new BufferedImageLuminanceSource(image, this.left + left, this.top + top, width, height);   
    }   
       
    @Override   
    public boolean isRotateSupported() {   
        return true;   
    }   
       
    @Override   
    public LuminanceSource rotateCounterClockwise() {   
        int sourceWidth = image.getWidth();   
        int sourceHeight = image.getHeight();   
        AffineTransform transform = new AffineTransform(0.0, -1.0, 1.0, 0.0, 0.0, sourceWidth);   
        BufferedImage rotatedImage = new BufferedImage(sourceHeight, sourceWidth, BufferedImage.TYPE\_BYTE\_GRAY);   
        Graphics2D g = rotatedImage.createGraphics();   
        g.drawImage(image, transform, null);   
        g.dispose();   
        int width = getWidth();   
        return new BufferedImageLuminanceSource(rotatedImage, top, sourceWidth - (left + width), getHeight(), width);   
        }   
    }  
```
#### 编写解析二维码的实现代码
```java
try {   
    MultiFormatReader formatReader = new MultiFormatReader();   
    String filePath = "C:/Users/Administrator/Desktop/testImage/test.jpg";   
    File file = new File(filePath);   
    BufferedImage image = ImageIO.read(file);;   
    LuminanceSource source = new BufferedImageLuminanceSource(image);   
    Binarizer binarizer = new HybridBinarizer(source);   
    BinaryBitmap binaryBitmap = new BinaryBitmap(binarizer);   
    Map hints = new HashMap();   
    hints.put(EncodeHintType.CHARACTER\_SET, "UTF-8");   
    Result result = formatReader.decode(binaryBitmap,hints);     
    System.out.println("result = "+ result.toString());   
    System.out.println("resultFormat = "+ result.getBarcodeFormat());   
    System.out.println("resultText = "+ result.getText());     
} catch (Exception e) {   
    e.printStackTrace();   
}  
```

现在运行后可以看到控制台打印出了二维码的内容

 