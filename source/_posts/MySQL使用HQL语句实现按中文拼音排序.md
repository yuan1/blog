---
title: MySQL使用HQL语句实现按中文拼音排序
date: 2017-12-3 10:13:46
tags: 数据库
---

MySQL 默认字符集是utf-8,如果想实现中文排序,就需要用convert(filedName using gbk) 实现,但现有的hibernate的hql不能支持此函数,Hibernate已经对此做了相应的方案解决。我们可以在Dialect注册一个数据库函数,java代码如下：

```java
import org.hibernate.Hibernate;  
import org.hibernate.dialect.MySQL5Dialect;  
import org.hibernate.dialect.function.SQLFunctionTemplate ;  
import org.hibernate.type.StringType;  

public class MySQL5LocalDialect extends MySQL5Dialect {  
 public MySQL5LocalDialect(){  
 super();  
 //registerFunction("convert", new SQLFunctionTemplate(Hibernate.STRING, "convert(?1 using ?2)") ); //Hibernate.STRING在Hibernate3.6.5.Final版本以下可以使用，因为在Hibernate4.0及以  
 //上的版本中，Hibernate.STRING已经不再使用了 可以使用  
 //registerFunction("convert", new SQLFunctionTemplate(new StringType(), "convert(?1 using ?2)") ); 代替   
 }  
}  
```

另外，在applicationContext.xml中或hibernate.hbm.xml中修改 数据库配置的Dialect：

```java
package.MySQL5LocalDialect   
<property name="hibernate.dialect">  
MySQL5LocalDialect的包路径  
</property>  
```

最后在HQL中使用convert方法, 例如: order by convert(name, ‘gbk’) , (“GBK”也可以是其他字符集),就ok啦!  
各种type：
```java
 public static final NullableType LONG = new LongType();  
 public static final NullableType SHORT = new ShortType();  
 public static final NullableType INTEGER = new IntegerType();  
 public static final NullableType BYTE = new ByteType();  
 public static final NullableType FLOAT = new FloatType();  
 public static final NullableType DOUBLE = new DoubleType();  
 public static final NullableType CHARACTER = new CharacterType();  
 public static final NullableType STRING = new StringType();  
 public static final NullableType TIME = new TimeType();  
 public static final NullableType DATE = new DateType();  
 public static final NullableType TIMESTAMP = new TimestampType();  
 public static final NullableType BOOLEAN = new BooleanType();  
 public static final NullableType TRUE\_FALSE = new TrueFalseType();  
 public static final NullableType YES\_NO = new YesNoType();  
 public static final NullableType BIG\_DECIMAL = new BigDecimalType();  
 public static final NullableType BIG\_INTEGER = new BigIntegerType();  
 public static final NullableType BINARY = new BinaryType();  
 public static final NullableType WRAPPER\_BINARY = new WrapperBinaryType();  
 public static final NullableType CHAR\_ARRAY = new CharArrayType();  
 public static final NullableType CHARACTER\_ARRAY = new CharacterArrayType();  
 public static final NullableType TEXT = new TextType();  
 public static final Type BLOB = new BlobType();  
 public static final Type CLOB = new ClobType();  
 public static final NullableType CALENDAR = new CalendarType();  
 public static final NullableType CALENDAR\_DATE = new CalendarDateType();  
 public static final NullableType LOCALE = new LocaleType();  
 public static final NullableType CURRENCY = new CurrencyType();  
 public static final NullableType TIMEZONE = new TimeZoneType();  
 public static final NullableType CLASS = new ClassType();  
 public static final NullableType SERIALIZABLE = new SerializableType(Serializable.class);  
 public static final Type OBJECT = new AnyType();  
 ```
 