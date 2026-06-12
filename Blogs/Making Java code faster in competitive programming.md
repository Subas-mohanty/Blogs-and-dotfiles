### Author : Subas Mohanty
### Date : 27-09-2025


```
	class Solution{
		static {
			Solution s = new Solution();
			for (int i = 0; i < 500; i++)
				s.function(new int[][]{{0,0},{0,0},{0,0}});
		}
	
		int function(int [][] arr){
			return 0;
		}
	}
```
#### You might have seen the above code block in the top leetcode submission of a problem or in competitive programming solution such as codeforces. But what does it do, what's the need of it ?

#### Let's understand this......

#### What's happening here ?
#### In java as we all know a static block runs only once when the class is loaded by the jvm.  So for every problem this part runs once and create a object of the Solution class before running any other part of the code.

#### But what is the benefit of it, isn't it making the code slower as an extra code is running before the actual solution code?
#### The answer is not really, instead it is making the code faster, how ?

#### In a java program, when the program loads in the `JVM(Java Virtual Machine)`, the JVM loads the `Solution` class and immediately the static blocks executes and create a object of the Solution class and calls the function multiple times with a dummy input.

#### At that exact time what is happening is before running anything else, the program is warming up(yes warming up) by running that method 500 times.
#### In Java, the JIT (Just-In-Time compiler) optimizes code after it runs a few times. Calling a method 500 times before using it ensures the method is "hot" (optimized) when real input comes.

#### Why this is used ?
#### In competitive programming, where execution time is critical, even small optimizations matter.
#### This static warm-up trick leverages JVM behavior to gain a slight performance edge.
## Read here to understand difference between JIT and Javac compiler [[Difference between Javac and JIT compiler]]