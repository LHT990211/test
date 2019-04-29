Validate

    作用是：当用户提交的信息格式错误时：会按照你在validate
    面设置好的信息提醒用户格式的错误。
    
一般Validate文件会放在controller文件夹里面
    
    在validate文件夹的php文件中一般都会默认先执行
    protected $rule = [
    ['name', 'require|max:10','分类名必须传递|分类名不能超过10个字符']，
    ]；
    
    
    如果你在php文件中定义了其他的变量名时，你在调用的时候，必须要去调用一个变量名
    /**场景设置**/
    protected $scene = [
        'add'  => ['name', 'parent_id'],//添加
        'listorder' => ['id', 'listorder'],//排序
    ]
    
在controller控制台调用时：

    $data = input('post.')//接收前端穿过来的信息
    $validate = validate('Category(在validate中的php文件名)')；
    $validate->check($data)//默认调用$rule
    $validate->scene('add')->check($data) //调用了scene里面的add
        
    