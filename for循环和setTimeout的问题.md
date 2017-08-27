# for循环和setTimeout()的问题

    for(var i=0; i<5; i++){
    	setTimeout(function(){
    		console.log(i);
    	},1000);
    }

上面的程序，按照我们最原始的理解，应当输出：0 1 2 3 4

然而结果并非我们想象中的或者说期待中的那样。而是打印出：4 4 4 4 4。   

为什么呢？

    for(var i=1; i<=5; i++){
	    setTimeout(function timer(){
	    	console.log(i);
	    },1000);
	    console.log(i);
    }
上面一段代码的输出结果是 1 2 3 4 5 6 6 6 6 6

最根本的原因应该是JS的单线程机制，意味着同一时间内只能执行一条语句，在这里，执行的顺序是：

1. var i=1; //事实上，这一步也分成两步去执行:声明和赋值
1. 判断i<5;
1. 1000ms后setTimout加入执行的队列
1. console.log(i);


解决这样的问题并得到想要的结果的一个方案是用一个立即执行函数来避免阻塞。
    
    for(var i=0; i<5; i++){
    	(function(i){
    		setTimeout(function(){
    			console.log(i);
    		},1000);
    	})(i);
    }

注意到，立即执行函数里面的i是用来干嘛的呢，《你不知道的JS》里面是这样说的：

它需要有自己的变量，用来在每个迭代中储存i的值。