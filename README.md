# Add Reading Minutes to Blog Posts
A way of displaying the reading minutes for each of your HubSpot blog posts.

<p align="center">
  <img src="https://github.com/ericsalvi/Add-Reading-Minutes-to-Blog-Posts/blob/master/images/reading-minutes-blog-post.png?raw=true" width="222" title="Reading Minutes">
</p>

## The Instructions
To display the reading minutes for each of your blog posts, you will want to add

`{{ content.post_body|wordcount|divide(300) }}` inside of the `{% for content in contents %}` section.

## The Breakdown
The first part, `content.post_body` is gathering all of the information from the post body. Pretty straightforward. Then appending the filter `wordcount` is telling us to get the total number of words in the post body. After that I then added `divide(300)` which will divide the wordcount by 300. Through seaching the Interent I found that the average adult human reads approximately 300 words per minute.

## The Why
The above code is the basis of how I came up with this snippet. I saw popular social platforms achieving this type of feature and wanted to replicate it in HubSpot. I had a good grasp on HubL for the blog markup and knew that if I were to come up with this same feature in HubSpot, I should be able to match it through HubL filters. However, through testing I realized that it was not rounding properly so an 899 word count for a blog post on paper would give us a result of 3 (899/300) but in actuallity it yeilded 2. I knew something was wrong. I had to come up with a better solution using my base code.

## The Updated Code
```
{% set initialPostWords = content.post_body|wordcount %}
{% set calculatedPostWords = (initialPostWords/100) * 100 %}
{% set finishedPostWords = calculatedPostWords|divide(300)|round(2) %}
{% set number = finishedPostWords|round %}
{% if number < 1 %}
 
{% else %}
  {{ finishedPostWords|round }} minute read
{% endif %}
```
Add these 8 lines of code in place of the initial one. What this will do is always round to the nearest 100. There also is a condition that if the final number is less than 1, It will not display anything. I felt that seeing `0 minute read` is not good for business. 

The only way you could get a 0 in these results would be if you have less than 150 words in your post or you have an infographic or video instead of text.

### Please Note

This will require you to make it look nice by using CSS. This snippet is only to get the foundation code present on your blog.

My original article was published on the [HubSpot Community](https://community.hubspot.com/t5/Share-Your-Work/How-to-Add-Reading-Minutes-to-Blog-Posts/m-p/9691#M30). 
