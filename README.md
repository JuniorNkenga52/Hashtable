# Hashtable
import java.util.Arrays;
public class HashSet implements Set {
 private Node[] data;
 private int size;
 private static final double LOAD_FACTOR=0.75;
 
 public HashSet(){
 data=new Node[13];
 size=0;
 }
 public boolean isEmpty(){return size==0;}
 
 public boolean remove(int b){
 int bucket=hash(b);
 if(data[bucket]==null)return false;
 if(data[bucket].data==b){
 data[bucket]=data[bucket].next;
 size--;
 return true;
 }else{
 Node a=data[bucket];
 while(a.next!=null){
 if(a.next.data==b){
 a.next=a.next.next;
 size--;
 return true;
 }
 a=a.next;
 }
 return false;
}
}
public String toString(){
String result="[";
for(int i=0; i<data.length; i++){
Node a=data[i];
while(a!=null){
 result+=a.data+", ";
 a=a.next;
 }
}
result=result.substring(0,result.length()-2);
return result+"]";
}
public void rehash(){
size=0;
Node[] x=data;
data=new Node[data.length*2];
for(int i=0; i<x.length; i++){
Node y=x[i];
while(y!=null){
  add(y.data);
  y=y.next;
  }
 }
}
public boolean contains(int b){
int bucket=hash(b);
Node a=data[bucket];
while(a!=null){
if(a.data==b)return true;
a=a.next;
}
return false;
}
 public void add(int b){
 if(contains(b)) return;
 if(size/data.length>=LOAD_FACTOR){
  rehash();
  }
  size++;
  int bucket=hash(b);
  data[bucket]=new Node(b,data[bucket]);
  }
public int size(){return size;}
 private int hash(int b){
 return b%data.length;
 }

 private class Node {
 private int data;
 private Node next;
 
 public Node(int data){
 this(data,null);
 }
 public Node(int data,Node next){
 this.data=data;
 this.next=next;
 }
}
}
