package datastructuer;


import java.text.ParseException;
import java.io.*;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.File;
import java.io.IOException;
import java.io.InputStream;
import java.util.Scanner;

public class Test {

    static double firstcal;
    static double secondval;
    
    public static void main(String[] args) throws Exception {
	    System.out.println("enter the first code path :");
	    firstcal=getpathandrun();
            System.out.println( firstcal);

	    System.out.println("enter the second code path :");
	    secondval=getpathandrun();
            System.out.println(secondval);
       if (secondval > firstcal){
           System.out.println("second code is later");

       }else 
           System.out.println("first code is later");

    	
    }

    
    public static double getpathandrun() throws Exception{

    	String passparam="";
       // String filePath ="C:\Users\PQ-CO\Documents\NetBeansProjects\shadi3";
        String filePath= new Scanner( System.in ).next();
    	StringFinder mystring= new StringFinder(filePath);
    	T myt=new T(filePath);
        try {
    	    System.out.println("first run javac filepath then enter any key+enter to continue:");

            String continuem= new Scanner( System.in ).next();
            
            //runProcess("javac Auto.java");
        	for(int i=0;i<10;i++){
	            String line=runProcess("java Auto "+i);
	            System.out.println(line);
	            String[] words = line.split("");
	            int count =0;
	            for (String word : words) {
	              if (word.equals("*")) {
	                count++;
	              }
	            }
	            passparam=passparam+"("+i+","+count+")"; 
	    	    System.out.println("Times found stars"+count);
        	}
        } catch (Exception e) {
            e.printStackTrace();
        }
        System.out.println("wait for answer:\n");
        String   passparamm="tool=lagrange-interpolating-polynomial&points="+passparam;
    	postm mm=new  postm();
    	String ans=mm.postm("https://www.dcode.fr/api/",passparamm,2000);

    	 String[] words = ans.split("\"");
         int count=10000;
         String math="";
         for (String word : words) {
           if (word.contains("f(x)")) {
        	   String[] words2 = word.split(" ");
        	   for (int i=0;i<words2.length-1;i++) {
        		 if (words2[i].contains("f(x)")) 
        			 count=i+1;
        		 if(i>count){
        			 math+=words2[i];
        		 }
               } 
               System.out.println("order is :"+math);
           }
         }
         
         check_the_order_amount ch=new check_the_order_amount();
        return ch.check_the_order_amount(math);
    }
    
    
    private static String runProcess(String command) throws Exception {
        Process pro = Runtime.getRuntime().exec(command);
        pro.waitFor();
        BufferedReader br = null;
		StringBuilder sb = new StringBuilder();
		String line;
		try {

			br = new BufferedReader( new InputStreamReader( pro.getInputStream()));
			while ((line = br.readLine()) != null) {
				sb.append(line);
			}

		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			if (br != null) {
				try {
					br.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
		return sb.toString();
    }

    
    
    private static void printLines(String name, InputStream ins) throws Exception {
        String line = null;
        BufferedReader in = new BufferedReader(
                new InputStreamReader(ins));
        while ((line = in.readLine()) != null) {
            System.out.println(name + " " + line);
        }
    }
}

 
