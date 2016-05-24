#java日常使用
1. 把ArrayList转换成数组
	
		ArrayList<Person> personList = new ArrayList<Person>();
		Person[] person = personList.toArray(new Person[personList.size()])
	
2. 把数组转换成ArrayList
	
		Person[] person = new Person[5];
		List<Person> list = new ArrayList<Person>(Arrays.asList(person));