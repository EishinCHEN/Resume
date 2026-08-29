<template>
  <div class="about-split-layout">
    <!-- 左半邊：角色基本身分與被動技能 (寬度約 45%) -->
    <div class="profile-panel">
      <!-- 角色名片 -->
      <div class="character-header">
        <div class="avatar-frame">
          <img src="@/assets/avatar.svg" alt="Avatar" class="avatar-img" />
        </div>
        <div class="title-box">
          <h3 class="char-name">陳映臻 (Eishin)</h3>
          <span class="char-title">全端/數據工程師</span>
        </div>
      </div>

      <!-- 🎓 學歷出身 -->
      <div class="section-box">
        <h4 class="section-title">🎓 學歷出身 (Education)</h4>
        <div class="info-card">
          <p class="main-text">東吳大學 - 日本語文學系</p>
          <span class="sub-text">2015 - 2019</span>
        </div>
      </div>

      <!-- 🎨 休閒活動 -->
      <div class="section-box">
        <h4 class="section-title">🪴 休閒活動 (Hobbies)</h4>
        <div class="hobby-tags">
          <span class="hobby-chip">🌱 綠色植栽</span>
          <span class="hobby-chip">🚴 單車騎行</span>
          <span class="hobby-chip">☕ 美食探索</span>
          <span class="hobby-chip">✈️ 海外自由行</span>
        </div>
      </div>
    </div>

    <!-- 右半邊：語言天賦與進修修練 (寬度約 55%) -->
    <div class="stats-panel">
      <!-- 🗣️ 語言能力 -->
      <div class="section-box">
        <h4 class="section-title">🗣️ 語言技能 (Languages)</h4>
        <div class="lang-group">
          <div class="lang-item">
            <div class="lang-info">
              <span>中文 (Native)</span>
              <span>100%</span>
            </div>
            <div class="bar-bg"><div class="bar-fill" style="width: 100%;"></div></div>
          </div>

          <div class="lang-item">
            <div class="lang-info">
              <span>日文 (JLPT /  N1)</span>
              <span>90%</span>
            </div>
            <div class="bar-bg"><div class="bar-fill" style="width: 90%;"></div></div>
          </div>

          <div class="lang-item">
            <div class="lang-info">
              <span>英文 (TOEIC / 715)</span>
              <span>70%</span>
            </div>
            <div class="bar-bg"><div class="bar-fill" style="width: 70%;"></div></div>
          </div>
        </div>
      </div>

      <!-- 📚 進修課程/技能強化 -->
      <div class="section-box">
        <h4 class="section-title">📚 技能修練 (Courses & Training)</h4>
        <ul class="training-list">
          <li>
            <strong class="course-name">Tibame C# 全端工程師養成班</strong>
            <span class="course-desc">C#、Vue、Javascript、jQuery</span>
          </li>
          <li>
            <strong class="course-name">華梵大學-AI大數據分析應用班</strong>
            <span class="course-desc">Python爬蟲、資料清洗、Tableau視覺化報表</span>
          </li>
          <li>
            <strong class="course-name">Google 數位人才探索計劃</strong>
            <span class="course-desc">Google Cloud、Gemini應用</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* 左右橫向佈局 */
.about-split-layout {
  display: flex;
  gap: 16px;
  width: 100%;
  align-items: stretch;
}

/* 面板共用塗鴉樣式 */
.profile-panel,
.stats-panel {
  background-color: #ffffff;
  border: 2.5px solid #5c2700;
  border-radius: 12px;
  padding: 16px;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.profile-panel { flex: 0 0 45%; }
.stats-panel { flex: 1; }

/* 角色標頭 */
.character-header {
  display: flex;
  align-items: center;
  gap: 12px;
  border-bottom: 2px dashed #937157;
  padding-bottom: 12px;
}

.avatar-frame {
  width: 52px;
  height: 52px;
  border: 2px solid #937157;
  border-radius: 60% 40% 70% 30% / 40% 50% 60% 50%;
  overflow: hidden;
  background-color: #f7f4f2;
  flex-shrink: 0;
}

.avatar-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.char-name {
  margin: 0;
  font-size: 16px;
  color: #5c2700;
}

.char-title {
  font-size: 12px;
  font-weight: bold;
  color: #937157;
}

/* 區塊標題 */
.section-title {
  margin: 0 0 6px 0;
  font-size: 13px;
  color: #5c2700;
}

/* 學歷資訊卡 */
.info-card {
  background-color: #f7f4f2;
  border: 1.5px solid #937157;
  border-radius: 8px;
  padding: 8px 10px;
}

.main-text {
  font-size: 12px;
  font-weight: bold;
  color: #5c2700;
  margin: 0;
}

.sub-text {
  font-size: 11px;
  color: #937157;
}

/* 被動技能 Tag */
.hobby-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.hobby-chip {
  font-size: 11px;
  font-weight: bold;
  color: #5c2700;
  background-color: #f7f4f2;
  border: 1.5px solid #5c2700;
  border-radius: 255px 15px 225px 15px/15px 225px 15px 255px;
  padding: 3px 8px;
}

/* 語言進度條 */
.lang-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.lang-info {
  display: flex;
  justify-content: space-between;
  font-size: 11px;
  font-weight: bold;
  color: #5c2700;
  margin-bottom: 2px;
}

.bar-bg {
  height: 8px;
  border: 1.5px solid #937157;
  border-radius: 6px;
  background: #f7f4f2;
  overflow: hidden;
  padding: 1px;
}

.bar-fill {
  height: 100%;
  background-color: #937157;
  border-radius: 4px;
}

/* 培訓列表 */
.training-list {
  padding-left: 16px;
  margin: 0;
  font-size: 12px;
  color: #5c2700;
}

.training-list li {
  margin-bottom: 6px;
}

.course-name {
  display: block;
  color: #5c2700;
}

.course-desc {
  font-size: 11px;
  color: #937157;
  display: block;
}
</style>