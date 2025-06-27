<h2 id="publications" style="margin: 2px 0px -15px;">
  Publications 
  (<span id="selectedBtn" class="pub-filter-btn active" onclick="showSelected()">Selected</span> / 
  <span id="fullBtn" class="pub-filter-btn" onclick="showFull()">Full</span>)
</h2>

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
.pub-filter-btn {
  cursor: pointer;
  transition: all 0.15s ease;
  font-weight: normal;
}

.pub-filter-btn:not(.active) {
  color: var(--global-theme-color, #002D72);
  text-decoration: underline;
}

.pub-filter-btn:not(.active):hover {
  color: var(--global-hover-color, #ffb81c);
}

.pub-filter-btn.active {
  color: var(--global-text-color, #000000);
  cursor: default;
  text-decoration: none;
}

@media (prefers-color-scheme: dark) {
  .pub-filter-btn:not(.active) {
    color: rgb(36, 150, 203);
  }
  
  .pub-filter-btn.active {
    color: #FFFFFF;
  }
}

.publication-item {
  transition: opacity 0.3s ease;
}

.publication-item.hidden {
  display: none;
}
</style>

<script>
function showSelected() {
  const selectedBtn = document.getElementById('selectedBtn');
  const fullBtn = document.getElementById('fullBtn');
  const nonSelectedPublications = document.querySelectorAll('.non-selected-publication');
  
  // 隐藏非精选论文
  nonSelectedPublications.forEach(item => {
    item.classList.add('hidden');
  });
  
  // 更新按钮状态
  selectedBtn.classList.add('active');
  fullBtn.classList.remove('active');
}

function showFull() {
  const selectedBtn = document.getElementById('selectedBtn');
  const fullBtn = document.getElementById('fullBtn');
  const nonSelectedPublications = document.querySelectorAll('.non-selected-publication');
  
  // 显示所有论文
  nonSelectedPublications.forEach(item => {
    item.classList.remove('hidden');
  });
  
  // 更新按钮状态
  selectedBtn.classList.remove('active');
  fullBtn.classList.add('active');
}

// 页面加载完成后默认显示精选论文
document.addEventListener('DOMContentLoaded', function() {
  showSelected();
});
</script>
