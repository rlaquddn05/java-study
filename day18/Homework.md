### day18.homework
```
package day18.homework;
/*
 *  1. 얕은 복사(Shallow Copy) : 객체를 복사할 때, 해당 객체만 복사하여 새 객체를 생성한다.
 *							    복사된 객체의 인스턴스 변수는 원본 객체의 인스턴스 변수와 같은 메모리 주소를 참조한다.
 *							    따라서, 해당 메모리 주소의 값이 변경되면 원본 객체 및 복사 객체의 인스턴스 변수 값은 같이 변경된다.
 *	
 * 	2. 깊은 복사(Deep Copy) : 객체를 복사 할 때, 해당 객체와 인스턴스 변수까지 복사하는 방식.
 *						       전부를 복사하여 새 주소에 담기 때문에 참조를 공유하지 않는다.
 */
class Person implements Cloneable { // clone() / copy()
	private String name;
	private int age;
	private Person father;
	private Person mother;
	
	
	public Person(String name, int age) {
		this.name = name;
		this.age = age;
	}
		
	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}
	
	public Person getFather() {
		return father;
	}

	public void setFather(Person father) {
		this.father = father;
	}

	public Person getMother() {
		return mother;
	}

	public void setMother(Person mother) {
		this.mother = mother;
	}
	
	@Override
	public Object clone() throws CloneNotSupportedException {
		return super.clone();
	}
	
	public void copy(Person daughtor) {
		daughtor.setFather(getFather());
		daughtor.setMother(getMother());
	}
		
}

public class Homework01 {
	public static void main(String[] args) throws CloneNotSupportedException {
		// 할아버지 : 홍길동 70세
		// 할머니 : 김피카츄 65세
		Person grandfather = new Person("홍길동",70);
		Person grandmother = new Person("김피카츄",65);
		// 어머니 : 김피츄 35세
		// 아버지 : 홍또도가스 40세
		Person father = new Person("홍또도가스", 40);
		father.setFather(grandfather);
		father.setMother(grandmother);
		Person mother = new Person("김피츄",35);
		// 아들 : 홍뚜벅초 10세
		// 딸 : 홍푸린 5세
		Person son = new Person("홍뚜벅초",10);
		son.setFather(father);
		son.setMother(mother);
		// 동일한 어머니, 아버지를 둔 뚜벅초, 푸린 생성 할 때
		// 푸린(동생) 객체를 생성할 때 깊은 복사를 해야하는지 얕은 복사를 해야하는지 생각해보고
		// 푸린객체는 뚜벅초 객체를 복사하여 구현하세요 . (아버지, 어머니가 뚜벅초와 같아야 함)
		// ==> 깊은복사를 해야한다. 복사 후 이름과 나이를 변경해야 하므로 얕은복사는 원본의 필드값을 바꿔버리기 때문		
		
		Person daughtor = new Person("홍푸린", 5);
		son.copy(daughtor);
						
//		Person daughtor = (Person)son.clone();	
//		daughtor.setName("홍푸린");
//		daughtor.setAge(5);
		
		System.out.println(son.getName());
		System.out.println(son.getAge());
		System.out.println(son.getFather().getName());
		System.out.println(son.getMother().getName());
		System.out.println("-------------------");
		System.out.println(daughtor.getName());
		System.out.println(daughtor.getAge());
		System.out.println(daughtor.getFather().getName());
		System.out.println(daughtor.getMother().getName());
		
	}
}
```
