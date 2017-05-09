# SimpleSale
A very very little beginner's project,just in order to learn how to use swing.
英语不好，下面还是用中文吧。

-----------------------------------
一、需要封装的类及其属性、方法
1、鸡  属性：price
      方法：getters&setters
2、肝  同鸡
3、胗  属性：quantity、price
      方法：getters&setters

4、分别继承JTable和defaultTableModel的两个类 属性：row column 
      方法：重写设置行列高度和宽度的方法，增加行、删除行的方法、单元格中设置获取值的方法
      
5、主窗口类   属性：鸡、肝、胗的列表（每次往数据库写完以后要清空）   table的成员变量   


二、数据库设计

create database SaleChicken;
use SaleChicken;

销售主表（下简称主表），用来存储每单交易的总金额、收、找情况，其中id被另三张表外键引用
create table mainsale (
id int primary key auto_increment,
kind int not null,      //1鸡 2鸡+胗 3鸡+肝 4鸡+胗+肝 5肝 6胗 7肝+胗 
totalcost double not null,
receive double not null,
gchange double not null,
inserttime datetime not null
);

鸡表，存储每只鸡的价钱，mid为主表的id
create table chicken (
id int primary key auto_increment,
mid int not null,   //主表的ID，鸡、肝、胗表里都应该有
price double not null,
inserttime datetime not null,
foreign key (mid) references mainsale(id)
);

肝表，存储每单肝的价钱，mid为主表的id
create table liver (
id int primary key auto_increment,
mid int not null,
price double not null,
inserttime datetime not null,
foreign key (mid) references mainsale(id)
);

胗表，存储每单胗的价钱，mid为主表的id
create table gizzard(
id int primary key auto_increment,
mid int not null,
price double,  //程序中默认为10元
quantity int, 
totalprice double,//总价钱
inserttime datetime,
foreign key (mid) references mainsale(id)
);
