 
### [(转)async中小结](http://jackyrong.iteye.com/blog/2186391)

**博客分类：**

*   [nodejs](http://jackyrong.iteye.com/category/333881)

 http://blog.csdn.net/sxyizhiren/article/details/18240435 

这里记录使用到的几个接口，给自己和需要的人参考。 

1.async.waterfall 

用法：async.waterfall(tasks, [callback]); 

task是函数组成的数组，callback是中途出错或者全部执行完后的回调函数。 

它的特点是串行执行函数，并且前一个函数的结果会传给下一个函数，比较类似Step模块的功能。 

我门看这是它readme中自带的例子： 
async.waterfall([ 
    function(callback){ 
        callback(null, 'one', 'two'); 
    }, 
    function(arg1, arg2, callback){ 
        callback(null, 'three'); 
    }, 
    function(arg1, callback){ 
        // arg1 now equals 'three' 
        callback(null, 'done'); 
    } 
], function (err, result) { 
   // result now equals 'done'    
}); 

其中第一个函数只有一个callback参数，callback是一定要有的，必须是最后一个参数。callback的作用是执行完一个函数后调用callback，然后就会进入下一个函数。如果你需要给第一个函数传递除callback外的参数怎么办？ 

如function(arg1,arg2,callback){} 

这里没有直接的方法，但是有间接的方法，就是把这个函数放到第二个的位置，根据waterfall的特点可以传参数给下一个函数，于是就可以在第一个函数里面把参数传给你的第二个函数了。 

那它是怎么传参数给下一个函数的呢？我们看到第一个函数调用了callback(null, 'one', 'two'); 

这里如果不是null而是err，那么这里的(null, 'one', 'two')就会紧接着传给waterfall的第二个参数，即async.waterfall(tasks, [callback])中的callback。 

这里是null就表示没有错误，所以就会紧着着调用第二个函数，同时第二个函数的参数是'one', 'two',callback.也就是它除去null，并在最后添加callback之后调用下一个函数. 

那么如果最后一个函数执行完了他会怎样。刚才我们讲了，如果一个函数返回err就直接进入到callback退出tasks中后续函数的执行，如果没有err就执行到tasks中最后一个函数了。那么最后一个函数不论它是否err，它内部调用callback(err,result1,result2...)中的所有参数都会如数传给async.waterfall(tasks, [callback])中的callback。中间不会再有加减参数的行为。 

2.async.mapSeries 

用法async.mapSeries(arr, iterator, callback) 

arr是一个数组，不能是一个json对象。 

作用的将arr中的每一项依次拿给iterator去执行，执行结果传给最后的callback 

例子： 

async.mapSeries([1,2,3,4], function(node,cb){cb(null,node+1);}, function(err,results){ 

console.log(results); 

//这里打印[2,3,4,5]，如果cb返回的结果有多个如cb(null,node+1,node+1,node+1,node+1)，那么结果将是这种形式的： 

//[[2,2,2,2],[3,3,3,3],[4,4,4,4],[5,5,5,5]] 

}); 

同样如果iterator中调用cb()都是传的null，所有arr中的元素都能得到执行，如果某个iterator传递err给cb()。那么将直接跳到callback中去，传给callback的是(err,results).这里results自然是不完整的，所以没有意义。 

3.async.mapLimit 

用法:mapLimit(arr, limit, iterator, callback) 

这个作用和mapSeries相似，唯一不同的是mapSeries是串行的，一个一个执行，而mapLimit可以同时执行limit个。 

你可能会问，node单线程怎么能同时执行多个呢？当然这里的多个是指多个需要callback等待的异步操作。mapSeries是等待上一个callback回来再执行这一个；mapLimit是同时发起多个异步操作，然后一起等待callback的返回，返回一个就再发起下一个。 

如果limit为1即mapLimit(arr, 1, iterator, callback)，就和mapSeries(arr, iterator, callback)的作用一样了。 

4.eachSeries 

用法eachSeries(arr, iterator, callback) 

作用类似mapSeries，也是串行执行，唯一不同的是，最后的callback只能收到err/null参数，不会返回每一次iterator的执行结果results. 

5.each 

用法：each(arr, iterator, callback) 

作用与eachSeries类似，最后也只能收到err/null作为反馈，但与eachSeries串行执行不同，each是全部执行并等待全部完成后返回，中间如果有错误就不等全部完成就立即返回。 

可以看到，函数名中有each的是没有结果集的，函数明名map是有结果集的； 

也可以看到,函数都是只要iterator返回err就立即调用callback返回。 

并且其内部有控制过，callback只会被调用一次，如果你发现被回调了多次，那么这一定是一个bug，可以向作者反馈。 

6.series 

用法series(tasks, [callback]) 

它的作用和waterfall相似，都是串行执行函数，都是一旦err就放弃后面的执行并回调callback。 

很大的差别是series中各个函数之间不传递参数,而是形成结果集。waterfall的callback全部成功时接收的是tasks中最后一个的回调结果。series中全部成功时接受的是每一个task的回调结果形成的数组。这个结果集可以参看上面的mapSeries中的结果集。 

因为不传递参数所以tasks中每个函数的参数只留下callback；因为接收结果集，所以callback的参数是(err,results).

例子： 

async.series([ 
    function(callback){ 
        // do some stuff ... 
        callback(null, 'one'); 
    }, 
    function(callback){ 
        // do some more stuff ... 
        callback(null, 'two'); 
    } 
], 
// optional callback 
function(err, results){ 
    // results is now equal to ['one', 'two'] 
});