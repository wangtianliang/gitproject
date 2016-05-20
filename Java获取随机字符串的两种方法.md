#【Java】获取随机字符串的两种方法
在做SQL测试或其他情况时，我们时常需要得到随机字符串。

在这里提供两种获取随机字符串的方法。

# 方法一
参数为字符串的长度。

	/** 产生一个随机的字符串*/  
	public static String RandomString(int length) {  
	    String str = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";  
	    Random random = new Random();  
	    StringBuffer buf = new StringBuffer();  
	    for (int i = 0; i < length; i++) {  
	        int num = random.nextInt(62);  
	        buf.append(str.charAt(num));  
	    }  
	    return buf.toString();  
	}  

# 方法二
【注】仅适用于JDK 1.7 。
参数同样为字符串的长度。
	
	/** 产生一个随机的字符串，适用于JDK 1.7 */  
	public static String random(int length) {  
	    StringBuilder builder = new StringBuilder(length);  
	    for (int i = 0; i < length; i++) {  
	        builder.append((char) (ThreadLocalRandom.current().nextInt(33, 128)));  
	    }  
	    return builder.toString();  
	}  

#优缺点比较

方法一可以产生给定字符串中可以出现的字符，但也只能出现这些字符。

方法二的方法体很简便，优点是生成的随机字符串中字符种类很多，缺点是只适用于JDK 1.7的版本。