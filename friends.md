---
layout: page
title: Friends
---
{% for friend in site.friends %}
<div class="friend-card">
	<a href="{{ friend.link }}" target="_blank" style="display: flex; align-items: center; text-decoration: none;">
		<img src="{{ friend.avatar }}" alt="{{ friend.name }}" style="width:48px; height:48px; border-radius:50%; margin-right:16px; vertical-align:middle;">
		<div style="display: flex; flex-direction: column; justify-content: center;">
			<strong style="font-size:1.2em;">{{ friend.name }}</strong>
			<div style="color:#888;">{{ friend.content | markdownify }}</div>
		</div>
	</a>
</div>
{% endfor %}

将你的信息以如下格式发送至我的邮箱：

```yaml
{
    name: "Stevezxc",
    link: "https://stevezxc.github.io/",
    avatar: "https://stevezxc.github.io/images/favicon.svg",
    description: "Ceaseless Seeker"
}
```
