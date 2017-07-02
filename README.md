# SimpleSale
A very very little beginner's project,just in order to learn how to use swing.

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
totalcost decimal(7,2) not null,
receive decimal(7,2) not null,
gchange decimal(7,2) not null,
inserttime datetime not null,
epay int default 0
);

明细表，存储订单下每件商品的具体信息，mid为主表的id
create table chicken (
id int primary key auto_increment,
mid int not null,   //主表的ID，鸡、肝、胗表里都应该有
type int not null,  //1鸡 2胗 3肝
quantity int, 
price decimal(7,2) not null,
inserttime datetime not null,
foreign key (mid) references mainsale(id)
);

需要添加一个电子支付的标志

