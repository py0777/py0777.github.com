title: "order_menu"
categories:

  - manage
tags: 
  - programming homework

    

toc: true
toc_sticky: true
toc_label: 목차
popular: true



우연히 대학 과제를 도와주는(?) 기회가 생겼다. 실무에서 하는 프로그래밍과 대학에서 배우는 프로그래밍은 조금 차이가 있기때문에 긴장되는 마음으로 프로그래밍을 해보았다. 제한된 정보를 받고, java 프로그램을 하는데, 생각보다 수월하게 풀 수 있었다. 문제가 생각보다 쉬웠을 수도 있지만, 구글 검색과 github를 조금 뒤져보니 비슷한 방식의 풀이가 여럿 있었다. 



실무에서 잘 사용하지도 않는 inner class와  downcasting 그리고 junit 설정등 말이다. 도와준다고 하곤 못하면 지인과 그 아들에게 부끄러울 뻔 했는데, 정말 다행이다.



\#### 과제 설명: Order 클래스 ##### 

__멤버변수__ 

\* Menu[] 타입의 멤버변수 orderList 를 가집니다. 접근 지정자는 private으로 설정 해줍니다.

 __생성자__ 

\* Order(Menu[] orderList) // 멤버변수 orederList를 입력 받은 배열로 초기화 합니다.

\* Order() // 멤버변수 orderList를 길이가 0인 배열로 초기화 합니다.

 __멤버함수__

 \* bill() // orderList에 들어있는 모든 객체를 가지고 메소드 getPrice()를 호출 하여, 그 값을 모두 더하여 리턴 합니다.

 \* waitingTime() // orderList에 있는 Menu 객체들 중에서 Food 클래스 타입으로 다운캐스팅이 가능한 객체들만 가지고 

​            메소드 getCookingTime()을 호출 하여, 그 값들을 모두 더하여 리턴 합니다.

* 다운캐스팅(downcasting)과 연산자(instanceof)를 사용하여 orderList에 있는 

​      임의의 객체가 Menu 객체이면서 동시에 Food 클래스 객체라면, Food 클래스 객체로 다운캐스팅하여

​      메소드 getCookingTime() 호출 리턴 값들을 더한 합계를 리턴함.



```java
class Menu{

	protected int price;
	
	public Menu(int price){
		this.price = price;
	}
	
	public Menu() {
		this.price = 0;
	}
	
	public int getPrice() {
		return price;
	}
	
	public void setPrice(int price) {
		this.price = price;
	}
	
}


class Food extends Menu{
	protected  int cookTime;
	
	public Food(int price, int cookTime){
		this.price = price;
		this.cookTime = cookTime;
	}
	
	public Food() {
		this.price = 0;
		this.cookTime = 0;
	}
	
	
	//Getter, Setter
	public int getCookTime() {
		return cookTime;
	}
	
	public void setCookTime(int cookTime) {
		this.cookTime = cookTime;
	}
}

class Juice extends Menu{
	private  String flavor ="Well";
	
	public Juice(int price, String flavor){
		this.price = price;
		this.flavor = flavor;
	}
	
	public Juice() {
		this.price = 0;
		this.flavor = "참외";
	}
	
	
	public String getFlavor() {
		return flavor;
	}
	
	public void setFlavor(String flavor) {
		this.flavor = flavor;
	}
}

/**
 * Order 클래스 
 *
 */
public class Order extends Menu {
	private Menu [] orderList; 
    
	Order(Menu[] orderList){	
		this.orderList = orderList;		
	}

	Order(){
		orderList = new Menu[0];
		
	}

    public int bill(){
    	
    	int sumBill = 0;
    	for(int i = 0 ; i < orderList.length ; i++) {
    		sumBill += orderList[i].getPrice();
    	}
    	
    	return sumBill;
    	
    }

    public  int waitingTime() {

    	 int cookTime = 0;
    	 for(int i = 0 ; i <orderList.length; i++) {
    		 if(orderList[i] instanceof Food) {
        		 Food food = (Food)orderList[i];
        		 cookTime += food.getCookTime();
        	 }	 
    	 }
    	 
    	 return cookTime;    	 
	 }
	
}

```

