---
layout: single
title: Contact
permalink: /contact/
author_profile: true

header:
  overlay_color: "#333"

excerpt: "Talk to me..."


locations: Renens,Switzerland

---

<body>
  <form action="https://formspree.io/chambrierg@gmail.com" method="POST">
       Name:
       <input type="text" name="Guillaume de Chambrier">
       Email:
       <input type="email" name="_replyto">
       Message:
       <textarea name="message"></textarea>
      <input type="submit" value="Send">
  </form>
</body>


# I AM HERE
{% if page.locations %}
<img src="http://maps.googleapis.com/maps/api/staticmap?{% for location in page.locations %}{% if forloop.first %}center={{location}}&markers=color:blue%7C{{location}}{% else %}&markers=color:blue%7C{{location}}{% endif %}{% endfor %}&zoom={% if page.zoom %}{{page.zoom}}{% else %}13{% endif %}&size=300x200&scale=2&sensor=false&visual_refresh=true" alt="">
{% endif %}
