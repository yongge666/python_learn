����ʹ��python������һ����ҳ��.

ʹ�÷���:

���������ȡ����ǰ��ҳ����

    current_page=int(request.GET.get("page",1))
�����ݿ���ȡ�����ܵļ�¼��

    item_list=models.���ݱ�.objects.all()
    total_item_count=item_list.count()

����һ��ҳ��Ķ���

    page_obj=Paginator(current_page,total_item_count,"/index/")

���巵�ص��ͻ��˵ļ�¼�б�

    item_list=models.���ݱ�.objects.all()[page_obj.start:page_obj.end]

���ʹ��render����redirect���ظ��ͻ���

    return render(request,"aaa.html",{"item_list":item_list,"page_html":page_obj.page_html()})
    


