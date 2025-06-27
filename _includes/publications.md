<h2 id="publications" style="margin: 2px 0px -15px;">Publications</h2>

<!-- 添加切换按钮 -->
<div style="margin: 20px 0;">
  <button id="publicationToggle" class="publication-toggle-btn" onclick="togglePublications()">
    Show Selected Publications
  </button>
  <span id="publicationCount" style="margin-left: 10px; color: #666; font-size: 14px;"></span>
</div>

<div class="publications">
<ol class="bibliography">

{% for link in site.data.publications.main %}

<li class="publication-item {% if link.selected %}selected-publication{% else %}non-selected-publication{% endif %}">
<div class="pub-row">
  <div class="col-sm-3 abbr" style="position: relative;padding-right: 15px;padding-left: 15px;">
    {% if link.image %} 
    <img src="{{ link.image }}" class="teaser img-fluid z-depth-1" style="width=100;height=40%">
    {% if link.conference_short %} 
    <abbr class="badge">{{ link.conference_short }}</abbr>
    {% endif %}
    {% endif %}
  </div>
  <div class="col-sm-9" style="position: relative;padding-right: 15px;padding-left: 20px;">
      <div class="title"><a href="{{ link.pdf }}">{{ link.title }}</a></div>
      <div class="author">{{ link.authors }}</div>
      <div class="periodical"><em>{{ link.conference }}</em>
      </div>
    <div class="links">
      {% if link.pdf %} 
      <a href="{{ link.pdf }}" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:14px;">Paper</a>
      {% endif %}
      {% if link.code %} 
      <a href="{{ link.code }}" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:14px;">Code</a>
      {% endif %}
      {% if link.page %} 
      <a href="{{ link.page }}" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:14px;">Homepage</a>
      {% endif %}
      {% if link.twitter %} 
      <a href="{{ link.twitter }}" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:14px;">Twitter</a>
      {% endif %}
      {% if link.bibtex %} 
      <a href="{{ link.bibtex }}" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:14px;">BibTex</a>
      {% endif %}
      {% if link.notes %} 
      <strong> <i style="color:#e74d3c"><b>{{ link.notes }}</b></i></strong>
      {% endif %}
      {% if link.others %} 
      {{ link.others }}
      {% endif %}
    </div>
  </div>
</div>
</li>
<br>

{% endfor %}

</ol>
</div>

<style>
.publication-toggle-btn {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.3s;
}

.publication-toggle-btn:hover {
  background-color: #0056b3;
}

.publication-item {
  transition: opacity 0.3s ease;
}

.publication-item.hidden {
  display: none;
}
</style>

<script>
let showingSelected = false;

function togglePublications() {
  const button = document.getElementById('publicationToggle');
  const countSpan = document.getElementById('publicationCount');
  const selectedPublications = document.querySelectorAll('.selected-publication');
  const nonSelectedPublications = document.querySelectorAll('.non-selected-publication');
  
  if (showingSelected) {
    // 切换到显示全部论文
    nonSelectedPublications.forEach(item => {
      item.classList.remove('hidden');
    });
    button.textContent = 'Show Selected Publications';
    countSpan.textContent = `(${selectedPublications.length + nonSelectedPublications.length} total)`;
    showingSelected = false;
  } else {
    // 切换到只显示精选论文
    nonSelectedPublications.forEach(item => {
      item.classList.add('hidden');
    });
    button.textContent = 'Show All Publications';
    countSpan.textContent = `(${selectedPublications.length} selected)`;
    showingSelected = true;
  }
}

// 页面加载完成后初始化计数
document.addEventListener('DOMContentLoaded', function() {
  const selectedPublications = document.querySelectorAll('.selected-publication');
  const nonSelectedPublications = document.querySelectorAll('.non-selected-publication');
  const countSpan = document.getElementById('publicationCount');
  countSpan.textContent = `(${selectedPublications.length + nonSelectedPublications.length} total)`;
});
</script>
