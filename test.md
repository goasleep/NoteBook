## Question1
``` java
double disabilityAmount() {
  if (!hasSeniority) {
    return 0;
  }
  if (isMonthsDisabled) {
    return 0;
  }
  if (isPartTime) {
    return 0;
  }
  // compute the disability amount
  //...
}
```
code smells:代码冗余  

Refactor:
```java
double disabilityAmount() {
  if (!hasSeniority || isMonthsDisabled || isPartTime) {
    return 0;
  }
}
```

## Question2
``` java
if (isSpecialDeal()) {
  total = price * 0.95;
  send();
}
else {
  total = price * 0.98;
  send();
}
```

code smells:代码冗余，应使用数字常量  

Refactor:
``` java
final double FIVE_PERCENT_OFF = 0.95;
final double TWO_PERCNET_OFF = 0.98; 
total = isSpecialDeal()?price * FIVE_PERCENT_OFF : price * TWO_PERCNET_OFF;
send()
```

## Question3
``` java
class Person {
  public String name;
}
```
code smells:数据没有封装  

Refactor:
``` java
class Person {
  private String name;
}
```

## Question4
``` java
class Student {
  public Set<String> getCourses() {return courses;}
  public void setCourses(Set<String> courses) {this.courses = courses;}
}
```

code smells:没有定义属性,没有格式化代码

Refactor:
``` java
class Student {
    private Set<String> courses = new Set<>();

    public Set<String> getCourses() {
        return courses;
    }

    public void setCourses(Set<String> courses) {
        this.courses = courses;
    }
}
```

## Question5
``` java
class Sun {
  private double temperature;
  public double getTemperature() {return this.temperature;}
  public void setTemperature(double temperature) {
  	this.temperature = temperature;
  }
}
```

code smells:没有格式化代码  
Refactor:
``` java

class Sun {
    private double temperature;

    public double getTemperature() {
        return this.temperature;
    }

    public void setTemperature(double temperature) {
        this.temperature = temperature;
    }
}
```

## Question6
``` java
void printOwing() {
  Enumeration elements = orders.elements();
  double outstanding = 0.0;

  // print banner
  System.out.println ("*****************************");
  System.out.println ("****** Customer totals ******");
  System.out.println ("*****************************");

  // print owings
  while (elements.hasMoreElements()) {
    Order each = (Order) elements.nextElement();
    outstanding += each.getAmount();
  }

  // print details
  System.out.println("name: " + name);
  System.out.println("amount: " + outstanding);
}
```
code smells:无效注释,代码冗余

Refactor:
``` java
void printOwing() {
  Enumeration elements = orders.elements();
  double outstanding = 0.0;

  System.out.println ("*****************************");
  System.out.println ("****** Customer totals ******");
  System.out.println ("*****************************");

  while (elements.hasMoreElements()) {
    outstanding += elements.nextElement().getAmount();
  }

  System.out.println("name: " + name);
  System.out.println("amount: " + outstanding);
}
```

## Question7
``` java
double price() {
  // Price consists of: base price - discount + shipping cost
  return quantity * itemPrice -
    Math.max(0, quantity - 500) * itemPrice * 0.05 +
    Math.min(quantity * itemPrice * 0.1, 100.0);
}
```

code smells:可读性差，魔法数字  

Refactor:
``` java
double price() {
  final double DISCOUNT_BASE_NUMBER = 500;
  final double DISCOUNT_MIN_NUMBER = 0；
  final double DISCOUNT_RATE = 0.05;
  final double SHIPPING_MAX_COST = 100;
  final double SHIPPING_COST_RATE = 0.1；
  double basePrice = quantity * itemPrice;
  double dicount = Math.max(DISCOUNT_MIN_NUMBER, quantity - DISCOUNT_BASE_NUMBER) * itemPrice * DISCOUNT_RATE；
  double shippingCost = Math.min(quantity * itemPrice * SHIPPING_COST_RATE, SHIPPING_BASE_COST);
  double price = basePrice - dicount + shippingCost;
  return price;
}
```


```
POST /parkingBoys/1 200
body{
  "parkingLots":[
    {"parkingLot": "123",
      "capacity" : "20"
    }
  ]
}
```

```
GET /parkingBoys 200
response body{
  "parkingBoys":[
    "parkingBoy":{
      "employeeID": "123",
      "parkingLots" : [
        "parkingLot" : "123",
        "capacity" : "20"
      ]
    }
  ]
}
```

```
POST /parkingOrder 200
body{
  "order":{
    "orderID":"123",
    "carID":"123"
  }
}
```

```
POST /parkingOrder 400
body{
  "order":{
    "orderID":"123",
    "carID":"123"
  }
}
```

```
Request:
POST /parkingBoy/1
body{
    "orderID":"123",
    "carID":"123"
}

Responed:
status:400
```

```
Request
POST /parkingOrder 200
body{
    "orderID":"123",
    "carID":"123"
}

Responed:
status 200
body{
    "orderID":"123",
    "carID":"123"
}
```

```
Request
POST /parkingOrder 200
body{
    "orderID":"123",
    "carID":"123"
}

Responed:
status 400
```

```
Request
GET /parkingOrder 200

Responed:
status 200
body{
  [
    "orderID":"123",
    "carID":"123"
  ]
}
```

create table `company` (
  `id` int auto)increment primary key,
  `name` varchar(255) not null,
)

create table `employee` (
  `id` int auto_increment primary key,
  `name` varchar(255) not null,
  `companyId` int not null
)