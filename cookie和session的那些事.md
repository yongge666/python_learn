���ھ���������������˵,����������һ�����:

���Ա��򾩶��̳ǵ���ҳ,��������˺ź�������е�½,Ȼ����й���,֧���Ȳ���������Ҫ�û��ٴ������û���������

��������û���һ����������ߵȼ���Сʱ����ˢ����Щ��ҳ���й������,�ͱ���Ҫ�ٴ������û�����������.

����Ϊʲô��??����õ���`cookie`��`session`��֪ʶ��.

**1. cookie�ļ��**

***1��http����״̬Э��,cookie������httpЭ�鷶Χ.***

��ʵ��Ӧ���У��������ͻ�����Ҫ��������״̬����ʱ����Ҫʹ�õ�cookie.

`cookie`�Ĺ���ԭ���ǣ��ɷ����������ͻ��������Ϣ���͸��ͻ��ˣ��ͻ����յ���Ϣ�󱣴��ڱ��أ�

���ͻ���������ٴη��ʷ����ʱ�����Զ�������������Ϣ��������ͨ�������Ϣ���жϿͻ��˵���ݡ�

***2��cookie��һ���̶��Ͻ����`"����״̬"`������***

����cookie�������֧��4096�ֽڣ�����cookie�����ڿͻ��ˣ����ܱ����ػ���ȡ,

�����Ҫ��һ���µĶ����������ֲ�cookie��һЩȱ�ݣ����ұ����ڷ���ˣ��нϸߵİ�ȫ��,�����session��

����httpЭ�����״̬��������������֪�������ߵ����,��ʱcookie�����Žӵ����á�

����˸�ÿ���ͻ��˵�cookie����һ��Ψһ�����id���û��ڷ��ʷ����ʱ��������ͨ��cookie���жϿͻ��˵���ݡ�

����˸���cookie��id�Ĳ�ͬ����һ���������ڱ���ͻ��˴��͹������˺�����ȹؼ���Ϣ.

***��cookie�ֲ���http��״̬�Ĳ��㣬�÷������ܹ��жϿͻ��˵����***

cookie���ı�����ʽ�����ڱ��أ�����ȫ�Խϲ�,��˷����ͨ��cookieʶ��ͬ���û�����Ӧ����session�ﱣ��˽�ܵ���Ϣ�Լ�����4096�ֽڵ��ı���

***4��cookie��session��ʵ�ǹ�ͨ�ԵĶ��������������ԺͿ��***

**2. cookie��session�Ĺ�������**

ÿ������ʹ��һ�����������һ����½ҳ���ʱ��һ������ͨ������֤,�������˾ͻᷢ��һ�����Ψһ���ַ�����������123abc�����������.

������洢��������˵Ķ����ͽ�`cookie`������������Ҳ��洢һ���û���ǰ��״̬������`login=true`��`username="name"`֮����û���Ϣ��

������Ϣ�����ֵ���ʽ�洢��Ϊһ���ַ������⴮�ַ������û���һ������ʱ�õ���cookieֵΪ��,�����session.

��ô����ڷ������˲鿴session��Ϣ�Ļ��������Ͼͻῴ���������ӵ����Ƶ��ֵ�

    {'123abc':{'login':true,'username':'hahaha'}}
    
��Ϊÿ��cookie����Ψһ����ģ�����������ͬһ̨�����ϻ���������ٵ�½ͬһ����վҲ��Ҫ�ٴ���֤��

��ôΪʲô˵����ֻ�������Ͽ������������Ƶ��ֵ��أ���Ϊ���ڰ�ȫ�ԵĿ��ǣ������ֵ�ڷ������˶��ᱻ���ܡ�

�������Ƿ������Ͼ����session��Ϣ������Ҳ���������������ӵĶ���:

    {'123abc':dasdasdasd1231231da1231231}
    
**3.cookie��session�ĳ���ʹ��**

����:����һ����½ҳ�棬�����ʹ��cookie��session��֤���û���������������ת����̨��ҳ�档

***3.1 ���ȴ���һ��Django����Ŀ,���ú�urls��settings,templates�д���һ��login.html��index.htmlҳ��***

views�еĴ���:
```
def index(request):
    return render(request,"index.html")

def login(request):
    print("cookie:",request.COOKIES)        #��ӡcookie��Ϣ
    
    if request.method=="POST":              #��������ʹ��post��ʽ�ύ��Ϣ
        name=request.POST.get("username")
        pwd=request.POST.get("password")
        
        if name=="hello" and pwd=="123456":
            return redirect("/index/")

    return render(request,"login.html")
```        
loginҳ��:
```
<form action="/login/" method="post">
    <p>����<input type="text" name="username"></p>
    <p>����<input type="password" name="password"></p>
    <p><input type="submit"></p>
</form>
```    
indexҳ��:

    <h3>welcome to index page</h3>
   
�������,����`http://127.0.0.1:8000/login/`��loginҳ��,������ȷ���û���������,����indexҳ��

��ʱ�����ں�˿������µ�cookie��Ϣ

    cookie: {'csrftoken': 'AdkajMM65wOqa0NONe6dVwYqphGNDOgMbuzstmAy92HJ3GxRWUNpqXKJFXBv1Rn5', 
    'sessionid': '7jfj6uqbz6vylplfv429bhfdxh14iwfp'}
    
����`sessionid`�е���Ϣ����Django������������һ������ַ���.

***3.2 ���û��Լ�����cookie��Ϣ***

�޸�login��ͼ����:

```
def login(request):

    print("cookie:",request.COOKIES)
    
    if request.method=="POST":
        name=request.POST.get("username")
        pwd=request.POST.get("password")
        
        if name=="hello" and pwd=="123456":
            res=redirect("/index/")
            res.set_cookie("login_message","hello python")#����cookie��Ϣ
            return res
            
    return render(request,"login.html")
```        
Ȼ������Ӧ��,���������û���������,����indexҳ��,��ʱ���Կ������µ�cookie��Ϣ:

    cookie: {'csrftoken': 'AdkajMM65wOqa0NONe6dVwYqphGNDOgMbuzstmAy92HJ3GxRWUNpqXKJFXBv1Rn5', 
    'sessionid': '7jfj6uqbz6vylplfv429bhfdxh14iwfp', 'login_message': 'hello python'}   
    
���Կ����ں�˵�login��ͼ���������õ�cookie�ļ�ֵ��,�����������ֻᱻ����˽���.

�û�����ҳ��ʱ,�Ǵ��ű�ʾ�Լ��������Ϣ��,����˶Կͻ��˵������Ϣ�����ж�,ֻ�������ȷ,���ܽ���indexҳ��.

���������������ĵ�ַ��ֱ������index��·�ɵ�ַ,Ҳ�ܽ���index��ҳ������,�ⲻ�������ǵ�Ҫ��.

***3.3 ʵ�ֿͻ���û��cookie,��ʹ�û�����index·����Ϣ,����˷��͵�¼ҳ����û�***

����ͻ���û��cookie,˵���û���������û����֤�ɹ�,����˾ͻ��loginҳ�淢�͸��ͻ��������,

ֻ���û�������ȷ���û���������,����˲Ż��indexҳ�淢�͸��ͻ��������.

�޸�index��ͼ����:
```
    def index(request):
        if request.COOKIES.get("login_message")=="hello python":
            return render(request,"index.html",locals())
        else:
            return redirect("/login/")
```
�����û���һ��������о�����֤����index.htmlҳ���,���cookie���߸���һ��������������indexҳ��,��Ҫ�ٴ���֤�û�����������.

�����û���cookie��Ϣ�����ڿͻ���,ÿ������ͨ��һ��,�ͻ��˾�Ҫ��cookie��Ϣ���;������һ��,���ұ����ڿͻ���Ҳ������ȫ,�����ֳ�����session

sessionҲ����ͻ�����ݵ���Ϣ,�û���¼�����˰ѱ�ʾ�û���ݵ���Ϣ������Լ�ֵ����ʽ���ڵ�session��,Ȼ�����˰�����ֵ䷢�͸��ͻ��˵�cookie,

��ʱ�ͻ��˵�cookie����һ���ַ�������ʽ����.

�ͻ���ʹ��cookie��session�����˽���ͨ�ŵĲ���:

    �û������û�����������֤��½��,����һ���ֵ�,���ֵ����session,session��key���Զ�����һ���ַ�����ʶ,Ҳ����ǰ��˵����cookie.
    ����˷��ظ��ͻ���session,session��value�洢���û��Ĺؼ���Ϣ,��user��iflogin��.
    
��Django���õ�sessionʱ,cookie�ɷ�����������,д���������cookie��,ÿ������������Լ���cookieֵ,��sessionѰ���û���Ϣ��Ψһ��ʶ

ÿ����������󵽺�̨���յ�request,��ʱ��session�ȼ��ڱ�ʶ�û������Ϣ���ֵ�

***3.4 ʹ��cookie��session��������������***

�޸�views�е�login��ͼ����
```
    def login(request):
        print("cookie:",request.COOKIES)
        print("session:",request.session)
    
        if request.method=="POST":
            name=request.POST.get("username")
            pwd=request.POST.get("password")
            if name=="hello" and pwd=="123456":
    
                res=redirect("/index/")
                res.set_cookie("login_message","hello python")
                return res
    
        return render(request,"login.html")
```
�ٴ�ˢ�������,������ȷ���û����������,��ӡcookie��session:

    cookie: {'csrftoken': 'AdkajMM65wOqa0NONe6dVwYqphGNDOgMbuzstmAy92HJ3GxRWUNpqXKJFXBv1Rn5', 
    'sessionid': '7jfj6uqbz6vylplfv429bhfdxh14iwfp', 'login_message': 'hello python'}
    
    session: <django.contrib.sessions.backends.db.SessionStore object at 0x00000000043D7D30>
    
���Կ������Ǵ�ʱ��session��һ������.

֪����`cookie`��`session`�������,��ô����ôʹ��cookie��session��

�޸���ͼ����
```
    def index(request):
        if request.session.get("is_login",None):#��ȡsession���û���¼����Ϣ
            name=request.session.get("user")#��ȡsession�е��û���
            return render(request,"index.html",locals())
        else:
            return redirect("/login/")
    
    def login(request):
        print("cookie:",request.COOKIES)
        print("session:",request.session)
    
        if request.method=="POST":
            name=request.POST.get("username")
            pwd=request.POST.get("password")
            
            if name=="hello" and pwd=="123456":
                request.session["is_login"]=True
                request.session["user"]=name
                return redirect("/index/")
        return render(request,"login.html")
 ```       
��ʹ��

    python manage.py makemigrations
    python manage.py migrate
    
�����ʼ�����ݿ�,Ȼ���������������`http://127.0.0.1:8000/index/`��,�����¼ҳ��,������ȷ���û���������,��˻��ӡ������Ϣ:

    cookie: {}
    session: <django.contrib.sessions.backends.db.SessionStore object at 0x00000000043B46D8>
    
**4.  cookie��session���÷�**

***4.1 ����cookie***

    ��ȡcookie            request.COOKIE[key]
    ����cookie            response.set_cookie(key,value)
    
����cookie�����ڿͻ��˵ĵ�����,����jQueryҲ���Բ���cookie

�������������,��htmlҳ���о�ʹ��Django���﷨������Ⱦname����.

����cookie��ʧЧʱ��:
```
    import datetime#����datetimeģ��
    
    response.set_cookie("username",{"11":"22"},max_age=10,
        expires=datetime.datetime.utcnow()+datetime.timedelta(days=3))
```     
����:

    datetime.datetime.utcnow()��ʾ��ǰʱ��
    datetime.timedelta(days=3)��ʾ3��
    
����Ĵ����ʾ����cookie�ڵ�ǰʱ���3���ʧЧ

***4.2 ����session(sessionĬ���ڷ���˱���15��)***

    ��ȡsession       request.session[key]����request.session.get(key)
    ����session       request.session[key]=value
    ɾ��session       del request.session[key]
    
��Ҫע�����,ɾ������˵�`session`����ɾ�����ݿ��е�`session_data`,��ֻ�ǰ�session����Ϊһ��������ֵ

����session��ʧЧʱ��:

    request.session.set_expiry(value)������session��ʧЧʱ��
    
����˵��:
   
    ���value��һ������,session���������ƺ�ʧЧ
    ���value�Ǹ�datatime����timedelta,session�������ʱ��֮��ʧЧ
    ���value��0,�û��ر��������session�ͻ�ʧЧ
    ���value��None,session������ȫ��session��ʧЧ����
