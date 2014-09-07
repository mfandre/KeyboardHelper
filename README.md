KeyboardHelper
==============

using System;
using System.Collections.Generic;
					
public class Program
{
	private static List<Tuple<Tuple<string,string>, int>> wordFrequency;
	
	public static void Main()
	{
		Console.WriteLine("Hello World");
		
		wordFrequency = new List<Tuple<Tuple<string,string>, int>>();
		
		String line = Console.ReadLine();
		analyseFrequency(line);
		printWordFrequency();
	}
	
	private static void analyseFrequency(String line){
		String[] words = line.Split(' ');
		//Console.WriteLine("0");
		int i,j;
		for(i = 0,j = 1; i < words.Length; i++, j++){
			//Console.WriteLine("0.5");
			if(j == words.Length){
				//Console.WriteLine("0.8");
				return;
			}
			
			Tuple<string,string> key = new Tuple<string,string>(words[i],words[j]);
			//Console.WriteLine("1");
			if(!checkTupleExists(key)){
				//Console.WriteLine("2");
				Tuple<Tuple<string,string>, int> item = new Tuple<Tuple<string,string>, int>(key,0);
				wordFrequency.Add(item);
				//Console.WriteLine("3");
			}
		}
	}
	
	private static bool checkTupleExists(Tuple<string,string> key){
		int i = 0;
		foreach(Tuple<Tuple<string,string>, int> item in wordFrequency){
			Tuple<string,string> words = item.Item1;
			if(words.Item1.Equals(key.Item1) && words.Item2.Equals(key.Item2)){
				wordFrequency[i] = new Tuple<Tuple<string,string>, int>(words, item.Item2 + 1);
				return true;
			}
			i++;
		}
		return false;
	}
	
	private static void printWordFrequency(){
		foreach(Tuple<Tuple<string,string>, int> item in wordFrequency){
			Tuple<string,string> words = item.Item1;
			Console.WriteLine(item.Item1.Item1 + " -> " + item.Item1.Item2 + "[" + item.Item2 + "]");
		}
	}
}
