# WinSoftAssignment

Que 1 }  Replace each array element by its corresponding rank
  Given an array of distinct integers, replace each array element by its corresponding rank in the array.
Ans : 

using System;
using System.Linq;

class Program
{
    static void Main(string[] args)
    {
        int[] arr = { 10, 8, 15, 12, 6, 20, 1 };
        int[] result = ReplaceWithRank(arr);
        Console.WriteLine("Output: {" + string.Join(", ", result) + "}");
    }

    static int[] ReplaceWithRank(int[] arr)
    {
        var sortedArr = arr.OrderBy(x => x).ToArray();
        var rankDict = sortedArr.Select((value, index) => new { value, index })
                                .ToDictionary(pair => pair.value, pair => pair.index + 1);
        return arr.Select(x => rankDict[x]).ToArray();
    }
}
--------------------------------------------------------------------------------------------------------------------------------------
Que 2 } Given a string s, find the length of the longest substring without repeating characters.
Ans :

using System;
using System.Collections.Generic;

class Program
{
    static void Main(string[] args)
    {
        string s1 = "abcabcbb";
        string s2 = "bbbbb";
        string s3 = "pwwkew";

        Console.WriteLine(LengthOfLongestSubstring(s1)); 
        Console.WriteLine(LengthOfLongestSubstring(s2));  
        Console.WriteLine(LengthOfLongestSubstring(s3)); 
    }

    static int LengthOfLongestSubstring(string s)
    {
        int maxLength = 0;
        Dictionary<char, int> seen = new Dictionary<char, int>();
        int start = 0;

        for (int i = 0; i < s.Length; i++)
        {
            if (seen.ContainsKey(s[i]) && start <= seen[s[i]])
            {
                start = seen[s[i]] + 1;
            }
            else
            {
                maxLength = Math.Max(maxLength, i - start + 1);
            }

            seen[s[i]] = i;
        }

        return maxLength;
    }
}

--------------------------------------------------------------------------------------------------------------------------------------
Que3 } Find non-repeating characters in a string.
Ans :

using System;
using System.Collections.Generic;

class Program
{
    static void Main(string[] args)
    {
        string s = "hello";
        List<char> nonRepeatingChars = FindNonRepeatingCharacters(s);

        Console.WriteLine("Non-repeating characters:");
        foreach (char c in nonRepeatingChars)
        {
            Console.WriteLine(c);
        }
    }

    static List<char> FindNonRepeatingCharacters(string s)
    {
        List<char> nonRepeatingChars = new List<char>();
        Dictionary<char, int> charCount = new Dictionary<char, int>();

        foreach (char c in s)
        {
            if (charCount.ContainsKey(c))
            {
                charCount[c]++;
            }
            else
            {
                charCount[c] = 1;
            }
        }

        foreach (KeyValuePair<char, int> pair in charCount)
        {
            if (pair.Value == 1)
            {
                nonRepeatingChars.Add(pair.Key);
            }
        }

        return nonRepeatingChars;
    }
}

--------------------------------------------------------------------------------------------------------------------------------------
Que 4 } You are given an array of integers. 
Write a C# program to find the frequency of each unique element in the array and 
store the results in a dictionary where the key is the element and the value is its frequency.
Then, print the elements and their frequencies.
Ans : 
using System;
using System.Collections.Generic;

class Program
{
    static void Main(string[] args)
    {
        int[] numbers = { 1, 2, 2, 3, 3, 3, 4, 4, 4, 4 };
        Dictionary<int, int> frequencyDict = CalculateFrequency(numbers);

        PrintFrequencies(frequencyDict);
    }

    static Dictionary<int, int> CalculateFrequency(int[] numbers)
    {
        Dictionary<int, int> frequencyDict = new Dictionary<int, int>();

        foreach (int num in numbers)
        {
            if (frequencyDict.ContainsKey(num))
            {
                frequencyDict[num]++;
            }
            else
            {
                frequencyDict[num] = 1;
            }
        }

        return frequencyDict;
    }

    static void PrintFrequencies(Dictionary<int, int> frequencyDict)
    {
        foreach (KeyValuePair<int, int> kvp in frequencyDict)
        {
            Console.WriteLine($"Element: {kvp.Key}, Frequency: {kvp.Value}");
        }
    }
}
