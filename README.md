# homework5.9

python manage.py shell

from django.contrib.auth.models import User 
User.objects.create_user('username1')
User.objects.create_user('username2')


from newsportal.models import Author

author1 = Author.objects.create(user=User.objects.get(pk=1))   
author2 = Author.objects.create(user=User.objects.get(pk=2))  


from newsportal.models import Category

category1=Category.objects.create(category='sport')

category2=Category.objects.create(category='politic')

category3=Category.objects.create(category='love')

category4=Category.objects.create(category='hobby')


from newsportal.models import Post     



article1 = Post.objects.create(type_of_post ='AL', author=Author.objects.get(pk=1), title='First article', body='first body')
article1.category.add(category1)

article2 = Post.objects.create(type_of_post ='AL', author=Author.objects.get(pk=2), title='Second article', body='second body')  
article2.category.add(category2)


news1 = Post.objects.create(type_of_post ='NW', author=Author.objects.get(pk=1), title='First news', body='First news body')    
news1.category.add(category3) 
news1.category.add(category4) 

from newsportal.models import Comment     

comment1=Comment.objects.create(post=article1, user=User.objects.get(pk=1), comment='first comment')   
comment2=Comment.objects.create(post=article2, user=User.objects.get(pk=2), comment='second comment')  
comment3=Comment.objects.create(post=news1, user=User.objects.get(pk=1), comment='third comment')     
comment4=Comment.objects.create(post=article1, user=User.objects.get(pk=1), comment='fourth comment')

comment1.like()
comment3.like()
comment2.like()
comment4.like()
comment1.like()
comment3.like()
comment2.like()
comment4.like()   

comment1.dislike()
comment3.dislike()
comment2.dislike()
comment4.dislike()

news1.like()
news1.like()
news1.dislike()

article1.like()
article2.like()

article1.like()
article2.like()

article1.like()
article2.like()

article1.dislike()
article2.dislike()


author1.update_rating()
author2.update_rating() 


first_rating_author= Author.objects.order_by('-rating').first()

print(f"""Best Author Username: {first_rating_author.user.username} Rating: {first_rating_author.rating}""") 




first_rating_post = Post.objects.order_by('-rating').first()

print(f"""Best Post Added: {first_rating_post.date_time_create},  Username author: {first_rating_post.author.user.username}, Rating post: {first_rating_post.rating}, Post title: {first_rating_post.title}, Post body: {first_rating_post.body}, Post preview: {first_rating_post.preview()} """) 

comments = first_rating_post.comment_set.all()    

for comment_single in comments:
	print(f"""Date: {comment_single.date_time_create}, User: {comment_single.user.username}, Rating: {comment_single.rating}, Comment: {comment_single.comment} """)
