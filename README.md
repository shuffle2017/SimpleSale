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
create table mainsale (

id int primary key auto_increment, 

receipt decimal(7,2) not null,

income decimal(7,2) not null,

gchange decimal(7,2) not null,

inserttime datetime not null,

epay int default 0
);    //0现金 1欠款  2支付宝  3微信



明细表，存储订单下每件商品的具体信息，mid为主表的id


create table detail(

id int primary key auto_increment,

mid int not null,   //主表的ID，外键引用主表
type int not null,  //1鸡 2胗 3肝

quantity int, 

price decimal(7,2) not null,

inserttime datetime not null,

foreign key (mid) references mainsale(id)
);



