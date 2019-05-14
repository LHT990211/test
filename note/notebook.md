```php
1.6反射


        面向对象编程中对象被赋予了自省的能力，而这个自省的过程就是反射
        
       一般会用到对象的时候是：
       1、对对象进行测试
       2、获取类的信息
        
    作用：
    
        反射可以用于文档生成。因此可以用它对文件里的类型进行扫描，逐个生成描述文档
        
        
构造方法__construct()

        1.PHP 构造方法 __construct() 允许在实例化一个类之前先执行构造方法。
        
        在一个类中只能声明一个构造方法，而是只有在每次创建对象的时候都会去
        调用一次构造方法，不能主动的调用这个方法，所以通常用它执行一些有用
        的初始化任务。该方法无返回值。
        
        2.PHP 析构方法 __destruct() 允许在销毁一个类之前执行执行析构方法。
        
        与构造方法对应的就是析构方法，析构方法允许在销毁一个类之前执行的
        一些操作或完成一些功能，比如说关闭文件、释放结果集等。析构函数不
        能带有任何参数，其名称必须是 __destruct() 。
 
       
__call()方法

        __call()方法。当调用一个没有在类中声明的方法时，可以调用__call()
        方法代替声明一个方法。接受方法名和数组作为参数。
        
        
Reflection 
       
       
        PHP Reflection API是PHP5才有的新功能，它是用来导出或提取出关于类、
        方法、属性、参数等的详细信息，包括注释。
        
        用得比较多的就只有两个ReflectionClass与ReflectionObject，两个的用
        法都一样，只是前者针对类，后者针对对象，后者是继承前者的类；然后
        其中又有一些属性或方法能返回对应的Reflection对象
        
      
1.7异常和错误的处理

    捕获异常的方式有两种：
        1、立刻捕获
        2、分散异常集中捕获
        
        
    错误常见的几种：
        1、deprecated（可正常运行）
            低级错误，表示“不推荐、不建议”
        2、notice（可正常运行）
            这种错误一般是语法中存在不当的地方
        3、warning（需修改）
            级别比较高的错误。
            语法中出现很不恰当的请况时会报此错误
        4、fetal error(需修改)
            致命错误
            
            
    错误的处理机制
    
        a、set_error_handler
            1、接管错误的处理
            2、设置用户自定义的错误处理函数，它需要先创建一个错误处理函数，语法如下
                set_error_handler(error_function,error_types)
                参数的描述：
                    error_function:规定发生错误时运行的函数。必需。
                    error_types：规定在那个错误报告级别会
                    
         自定义的错误处理函数一定要有这四个输入变量$errno、$errstr、$errfile、$errline.
                
        b、trigger_error
            主动抛出一个错误
            
            
            function customError($errno, $errstr, $errfile, $errline)
            {
                //自定义错误处理时，手动抛出异常
                throw new Exception($level .'|'.${errstr});
            }
            set_error_handler("customError",E_ALL|E_STRICT);
            try
            {
                $a = 5/0;
            }
            catch (Exception $e)
            {
                echo '错误信息：',$e ->getMessage();
            }
            
    
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        