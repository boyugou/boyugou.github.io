<h2 id="publications" style="margin: 2px 0px 10px;">Publications</h2>

<div class="publication-filter">
  <span id="selectedBtn" class="filter-tab active" onclick="showSelected()">Selected</span>
  <span id="fullBtn" class="filter-tab" onclick="showFull()">Full</span>
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
/* Publication filter styles */
.publication-filter {
  margin-bottom: 1.5rem;
  border-bottom: 1px solid #e8e8e8;
  display: flex;
  gap: 0;
}

.filter-tab {
  padding: 8px 16px;
  cursor: pointer;
  font-size: 0.95rem;
  font-weight: 500;
  border-bottom: 2px solid transparent;
  transition: all 0.2s ease;
  position: relative;
  top: 1px;
}

.filter-tab:not(.active) {
  color: var(--global-text-color-light, #828282);
}

.filter-tab:not(.active):hover {
  color: var(--global-theme-color, #002D72);
}

.filter-tab.active {
  color: var(--global-theme-color, #002D72);
  border-bottom-color: var(--global-theme-color, #002D72);
  cursor: default;
}

.publication-item {
  transition: opacity 0.3s ease;
}

.publication-item.hidden {
  display: none;
}

/* Unified Description List Styles */
.description-list {
  margin: 2rem 0;
}

.description-item {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 1.2rem;
  padding-bottom: 1.2rem;
  border-bottom: 1px solid #f0f0f0;
}

.description-item:last-child {
  border-bottom: none;
  margin-bottom: 0;
  padding-bottom: 0;
}

.description-term {
  flex: 0 0 160px;
  padding-right: 2rem;
  font-weight: 600;
  color: var(--global-text-color, #000000);
  font-size: 0.95rem;
}

.description-details {
  flex: 1;
  line-height: 1.5;
  color: var(--global-text-color-light, #828282);
  font-size: 0.95rem;
}

.description-details strong {
    font-weight: 600;
    color: var(--global-text-color, #000000);
}

.github-badge {
  height: 20px;
  vertical-align: middle;
}

/* Dark mode adjustments */
@media (prefers-color-scheme: dark) {
  .publication-filter {
    border-bottom-color: #404040;
  }
  
  .filter-tab:not(.active) {
    color: #999999;
  }
  
  .filter-tab:not(.active):hover {
    color: rgb(36, 150, 203);
  }
  
  .filter-tab.active {
    color: rgb(36, 150, 203);
    border-bottom-color: rgb(36, 150, 203);
  }

  .description-item {
    border-bottom-color: #404040;
  }
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .description-item {
    flex-direction: column;
  }
  .description-term {
    flex-basis: auto;
    padding-right: 0;
    margin-bottom: 0.5rem;
  }
}
</style>

<script>
function showSelected() {
  const selectedTab = document.getElementById('selectedBtn');
  const fullTab = document.getElementById('fullBtn');
  const nonSelectedPublications = document.querySelectorAll('.non-selected-publication');
  
  // 隐藏非精选论文
  nonSelectedPublications.forEach(item => {
    item.classList.add('hidden');
  });
  
  // 更新tab状态
  selectedTab.classList.add('active');
  fullTab.classList.remove('active');
}

function showFull() {
  const selectedTab = document.getElementById('selectedBtn');
  const fullTab = document.getElementById('fullBtn');
  const nonSelectedPublications = document.querySelectorAll('.non-selected-publication');
  
  // 显示所有论文
  nonSelectedPublications.forEach(item => {
    item.classList.remove('hidden');
  });
  
  // 更新tab状态
  selectedTab.classList.remove('active');
  fullTab.classList.add('active');
}

// 页面加载完成后默认显示精选论文
document.addEventListener('DOMContentLoaded', function() {
  showSelected();
});
</script>
