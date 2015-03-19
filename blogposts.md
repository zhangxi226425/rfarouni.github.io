---
layout: default
title : Blog Posts
header : Posts
group: navigation
---

<div class="page-header-wrapper">
	<div class="page-header">
<h1>{{ page.title }} {% if page.tagline %} <small>{{ page.tagline }}</small>{% endif %}</h1>
<!-- <table border="0"  style="width:100%">
<tr>
<td> 	
</td>
<td>
<form action="http://www.google.com/cse" id="cse-search-box">
  <p>
    <input type="hidden" name="cx" value="015077698314123965974:-r7xbwrv0ai" />
    <input type="hidden" name="ie" value="UTF-8" />
    <input type="text" name="q" id="cse-search-field" placeholder="Search" />
  </p>
</form>

</td>
</tr>
</table>
<script type="text/javascript" src="http://www.google.com/cse/cse.js?cx=015077698314123965974:-r7xbwrv0ai;lang=en"></script>
<script type="text/javascript">
var search_field = document.getElementById('cse-search-field');
search_field.style.background = null;
if (window.rsmsHostIsIOS) {
  search_field.type = 'search';
} else {
  search_field.select();
  search_field.focus();
}
search_field.addEventListener('blur', function (ev) {
  this.style.background = null;
});
</script> -->
</div >
</div >


<div class="posts">
  <div class="content.b full-bleed" id="recent-posts">
  {% for post in site.posts limit:25 %}<a
    href="{{ post.url }}" class="post-excerpt{% if post.photo_url %} photo{% endif %}">
      <div class="padded-content">
        <div class="title">{{ post.title }}</div>
      {% if post.photo_url %}
        <div class="image" style="background-image:url('{{ post.photo_url }}')"></div>
      {% else %}
        <!-- <div class="title">{{ post.title }}</div> -->
        <info datetime="{{ page.date | date: "%Y-%m-%d" }}">
          {{ post.date | date: "%b %Y" }}
        </info>
        {% if post.description %}
        <span class="body">{{ post.description | strip_html }}</span>
        {% else %}
        <span class="body">{{ post.excerpt | strip_html }}</span>
        {% endif %}
      {% endif %}<!-- post.photo_url -->
      </div>
    </a>{% endfor %}
    <div class="breaker"></div>
    <div class="end">
<!--    <a href="/archive/">More...</a> -->
    </div>
  </div>
</div>
<script type="text/javascript">
(function(f){
  var onload = function(f) {
    if (window.addEventListener) {
      window.addEventListener('DOMContentLoaded', f, false);
    } else {
      window.attachEvent('onload', f);
    }
  };
  onload(function(){
    f();
    if (window.addEventListener) {
      window.addEventListener('resize', f, false);
    } else {
      window.attachEvent('resize', f);
    }
  });
})(function(){
  var winw = window.innerWidth, w; //, width_thresholds = [680, 780];
  w = window.__post_grid_width;

  if ( (w !== undefined) &&
       ( (w === 680 && winw < 680) ||
         (w === 780 && winw >= 680 && winw < 780) ||
         (w === 10000 && winw >= 780)
       )
     )
  {
    // console.log('noop w:', w+ ', winw:', winw);
    return;
  } else {
    window.__post_grid_width = w =
      winw > 780 ? 10000 :
      winw > 680 ? 780 :
                   680;
    // console.log('op w:', w);
  }

  var posts = document.getElementById('recent-posts');
  var child_nodes = posts.childNodes, k, node, h,
      col_width, col0_y, col1_y, col1_x,
      origin = {x:0, y:0}, node_count = 0, is_col0, row0_max_y;

  posts.style.position = (window.__post_grid_width <= 680) ? null : 'relative';

  for (k in child_nodes) {
    node = child_nodes[k];
    if (node.nodeType === Node.ELEMENT_NODE) {
      if (node.className === 'breaker') {
        if (window.__post_grid_width <= 680) {
          node.style.height = null;
        } else {
          node.style.height = (Math.max(col0_y, col1_y) - row0_max_y) + 'px';
        }
        break;
      }
      if (col0_y === undefined) {
        origin.x = node.offsetLeft;
        origin.y = node.offsetTop;
        col_width = node.clientWidth;
        col0_y = origin.y + node.clientHeight;
        row0_max_y = col0_y;
      } else {
        if (col1_y === undefined) {
          col1_y = origin.y + node.clientHeight;
          col1_x = origin.x + node.clientWidth;
          if (col1_y > row0_max_y) {
            row0_max_y = col1_y;
          }
        } else {
          if (window.__post_grid_width <= 680) {
            // console.log('Clear');
            node.style.position = null;
            node.style.width = null;
            node.style.left = null;
            node.style.top = null;
          } else {
            is_col0 = (node_count % 2) === 0;
            node.style.position = 'absolute';
            node.style.width = col_width + 'px';
            if (is_col0) {
              node.style.left = origin.x + 'px';
              node.style.top = col0_y + 'px';
              col0_y += node.clientHeight;
            } else {
              node.style.left = col1_x + 'px';
              node.style.top = col1_y + 'px';
              col1_y += node.clientHeight;
            }
          }
          // console.dir(node);
        }
      }
      ++node_count;
    }
  }

});
</script>



 