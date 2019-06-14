碟片租赁商店管理系统
===
简介
-----
>本项目是为了熟练掌握CPP面向对象编程的思想而做的练习，该项目为碟片租赁商店进行了设计，店主使用这套系统可以在客户在DVD商店进行消费后，根据用户所借的不同的DVD种类和数量来计算用户消费的金额和积分。
   
目录介绍
--
```
├── Readme.md                  
├── head file                      
│   ├── Customer.h
│   ├── Movie.h                            
│   └── Rental.h              
├── source file                  
│   ├── Customer.cpp
│   ├── Movie.cpp  
│   ├── MoiveRental.cpp     
│   └── Rental.cpp
```
快速开始
--
>本项目使用的是C++编程语言，开发环境为Windows10下的Visual Studio编译器。在实际开发中主要运用到了代码重构的思想.<br>首先对电影类进行了实现，在Movie类中有电影的种类（静态常量）：普通电影、儿童电影、新电影，然后有两个成员变量/常量是priceCode（价格代码）、title（电影名称）
``` cpp
class Movie
{
private: 
	string	_title;
	int	_priceCode;
	Price	*_price;
public:
	enum PriceCode { REGULAR = 0, NEW_RELEASE, CHILDREN };
	Movie(string title, int priceCode);
	~Movie();
	int getPriceCode()const;
	void setPriceCode(int pc);
	string getTitle()const;
	double getCharge(int daysRented);
	int getFrequentRenterPoints(int daysRented);
};
```
>实现完Movie类接下来就是租赁类Rental，这个Rental类的职责就是负责统计某个电影租赁的时间。下方就是这个租赁类，该类也是比较简单的，其中有两个字段，一个是租了的电影，另一个就是租赁的时间了。
``` cpp
class Rental
{
private:
	Movie _movie;
	int _daysRented;
public:
	Rental(Movie movie, int daysRended)
		:_movie(movie), _daysRented(daysRended){}
	Movie* getMovie();
	int getDaysRented();
	double getCharge();
	int getFrequentRenterPoints();
};
```
>接下来要实现我们的消费者类了，也就是Customer类。在Customer类中有消费者的名字name和一个数组，该数组中存放的就是租赁电影的集合。其中的statement()方法就是结算该客户的结算信息的方法，并将结果进行打印。在此我们需要了解的需求是每种电影的计价方式以及积分的计算规则。
测试。
>电影价格计算规则：

>>普通片--2天之内含2天，每部收费2元，超过2天的部分每天收费1.5元

>>热销片--每天每部3元　

>>儿童片--3天之内含3天，每部收费1.5元，超过3天的部分每天收费1.5元

>积分计算规则：

>>每借一部电影积分加1，新片每部加2
``` cpp
int main()
{
	Movie spider = Movie("spider man", Movie::NEW_RELEASE);
	Rental *renter = new Rental(spider, 5);
	Customer may = Customer("may");
	Customer bye = Customer("bye");
	may.addRental(renter);
	may.addRental(renter);
	may.addRental(renter);
	may.addRental(renter);
	may.addRental(renter);
	may.addRental(renter);
	bye.addRental(renter);
	cout << may.statement() << endl;
	cout << bye.statement() << endl;
	cin.get();
	return 0;
}

```
--
测试
--
>

讨论
--
>该项目运用到了C++中重构的思想，重构：对软件内部结构的一种调整，目的是再不改变软件的可观察行为的前提下，提高其可理解性，降低其修改成本。
