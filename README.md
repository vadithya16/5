import java.lang.*;
import java.io.*;
import java.util.*;
class common
{
boolean flag=false;
String str;
public synchronized void produce()throws Exception
{
if(flag==false)
{
Scanner sc=new Scanner(System.in);
System.out.println("enter the string");
str=sc.next();
flag=true;
notify();
}
else
wait();
}
public synchronized void consume() throws Exception
{
if(flag==true)
{
System.out.println("the produced string by producer is : "+str);
flag=false;
notify();
}
else
}
}
wait();
class producer extends Thread
{
common c;
producer(common c)
{ this.c=c; }
public void run()
{
try
{
c.produce();
}catch(Exception e){}
}
}
class consumer extends Thread
{
common c;
consumer(common c)
{ this.c=c; }
public void run()
{
try
{ c.consume(); }catch(Exception e){}
}
}
public class pc
{
public static void main(String args[]) throws Exception
{
common c=new common();
producer p=new producer(c);
consumer co=new consumer(c);
p.start();
co.start();
}
}
