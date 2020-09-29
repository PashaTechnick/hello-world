# hello-world
Just repository

Hi!!!
My name is Pavel.
I am learning to programm in Java.

_____________________________________________
package com.javarush.task.task17.task1721;

import java.io.*;
import java.util.ArrayList;
import java.util.List;

/* 
Транзакционность
*/

public class Solution {
    public static List<String> allLines = new ArrayList<String>();
    public static List<String> forRemoveLines = new ArrayList<String>();
    public static String firstFileName;
    public static String secondFileName;

    static {
        try {
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            firstFileName = br.readLine();
            secondFileName = br.readLine();
        }catch (IOException e){
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        String str;
        try {
            BufferedReader firstFile = new BufferedReader(new FileReader(firstFileName));
            while ((str=firstFile.readLine())!=null){
                allLines.add(str);
            }
            firstFile.close();

            BufferedReader secondFile = new BufferedReader(new FileReader(secondFileName));
            while ((str=secondFile.readLine())!=null){
                forRemoveLines.add(str);
            }
            secondFile.close();
            new Solution().joinData();
        }
        catch (IOException e){
            e.printStackTrace();
        }
    }

    public void joinData() throws CorruptedDataException {
        if (allLines.containsAll(forRemoveLines)){
            allLines.removeAll(forRemoveLines);
        }
        else {
            allLines.clear();
            new CorruptedDataException();
        }
    }

}
