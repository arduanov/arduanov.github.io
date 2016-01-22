---
layout: post
---

PostgreSQL 9.4 improves a lot with the introduction of to_json, json_build_object, json_object and json_build_array, though it's verbose due to the need to name all the fields explicitly:

{% highlight sql %}
select
        json_build_object(
                'id', u.id,
                'name', u.name,
                'email', u.email,
                'user_role_id', u.user_role_id,
                'user_role', json_build_object(
                        'id', ur.id,
                        'name', ur.name,
                        'description', ur.description,
                        'duty_id', ur.duty_id,
                        'duty', json_build_object(
                                'id', d.id,
                                'name', d.name
                        )
                )
    )
from users u
inner join user_roles ur on ur.id = u.user_role_id
inner join role_duties d on d.id = ur.duty_id;

{% endhighlight %}
