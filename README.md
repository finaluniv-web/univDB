[index.html](https://github.com/user-attachments/files/26664386/index.html)
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>동국대 체교과 실기 기록</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: 'Apple SD Gothic Neo', 'Noto Sans KR', sans-serif;
  background: #f0f4f8;
  min-height: 100vh;
}

/* ── 공통 헤더 ── */
.header {
  background: linear-gradient(135deg, #1a237e 0%, #1565c0 100%);
  color: white;
  padding: 36px 20px 28px;
  text-align: center;
}
.header h1 { font-size: 22px; font-weight: 800; margin-bottom: 6px; }
.header p  { font-size: 13px; opacity: 0.8; }

/* ── 메인 페이지 ── */
#mainPage { display: block; }
#detailPage { display: none; }

/* ── 학생 그리드 ── */
.container {
  max-width: 480px;
  margin: 0 auto;
  padding: 20px 16px 60px;
}
.section-title {
  font-size: 12px;
  font-weight: 700;
  color: #aaa;
  letter-spacing: 1px;
  margin-bottom: 14px;
}
.student-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 10px;
}
.student-card {
  background: white;
  border-radius: 16px;
  padding: 16px 10px;
  text-align: center;
  cursor: pointer;
  box-shadow: 0 2px 10px rgba(0,0,0,0.06);
  transition: transform 0.15s, box-shadow 0.15s;
  border: 2px solid transparent;
}
.student-card:active {
  transform: scale(0.96);
  box-shadow: 0 1px 6px rgba(0,0,0,0.1);
}
.student-card.male-card:hover   { border-color: #3949ab; }
.student-card.female-card:hover { border-color: #e91e63; }

.avatar {
  width: 48px; height: 48px;
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 22px;
  margin: 0 auto 10px;
}
.male-avatar   { background: #e8eaf6; }
.female-avatar { background: #fce4ec; }

.student-name {
  font-size: 14px;
  font-weight: 700;
  color: #1a1a2e;
  margin-bottom: 4px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.student-school {
  font-size: 10px;
  color: #bbb;
  margin-bottom: 6px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.gender-badge {
  display: inline-block;
  padding: 2px 8px;
  border-radius: 20px;
  font-size: 10px;
  font-weight: 700;
}
.male-badge   { background: #e8eaf6; color: #3949ab; }
.female-badge { background: #fce4ec; color: #e91e63; }

/* ── 상세 페이지 헤더 ── */
.detail-header {
  background: linear-gradient(135deg, #1a237e 0%, #1565c0 100%);
  color: white;
  padding: 32px 20px 24px;
  text-align: center;
  position: relative;
}
.back-btn {
  position: absolute;
  left: 16px; top: 50%;
  transform: translateY(-50%);
  color: white;
  font-size: 24px;
  cursor: pointer;
  opacity: 0.85;
  background: none;
  border: none;
  padding: 8px;
}
.detail-school { font-size: 11px; opacity: 0.7; margin-bottom: 4px; letter-spacing: 0.5px; }
.detail-name   { font-size: 26px; font-weight: 800; margin-bottom: 4px; }
.detail-sub    { font-size: 13px; opacity: 0.8; }
.detail-badge  {
  display: inline-block;
  margin-top: 10px;
  padding: 4px 14px;
  background: rgba(255,255,255,0.18);
  border-radius: 20px;
  font-size: 12px;
  font-weight: 600;
}

/* ── 탭 ── */
.tab-wrap {
  background: white;
  display: flex;
  border-bottom: 2px solid #e8eaf6;
  position: sticky;
  top: 0;
  z-index: 10;
}
.tab-btn {
  flex: 1;
  padding: 14px 0;
  text-align: center;
  font-size: 13px;
  font-weight: 600;
  color: #aaa;
  cursor: pointer;
  border: none;
  border-bottom: 3px solid transparent;
  background: none;
  transition: all 0.2s;
}
.tab-btn.active { color: #1a237e; border-bottom: 3px solid #1a237e; }

/* ── 공식테스트 배너 ── */
.official-banner {
  background: linear-gradient(135deg, #1a237e, #283593);
  border-radius: 20px;
  padding: 20px;
  color: white;
  margin-bottom: 16px;
}
.official-title { font-size: 11px; opacity: 0.7; letter-spacing: 1px; margin-bottom: 4px; }
.official-date  { font-size: 14px; font-weight: 700; margin-bottom: 16px; opacity: 0.9; }
.official-grid  { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.official-item  { background: rgba(255,255,255,0.12); border-radius: 12px; padding: 12px; }
.oi-label { font-size: 11px; opacity: 0.75; margin-bottom: 4px; }
.oi-value { font-size: 20px; font-weight: 800; }
.oi-unit  { font-size: 11px; opacity: 0.7; margin-left: 2px; }
.oi-score {
  margin-top: 6px;
  font-size: 11px;
  background: rgba(255,255,255,0.15);
  border-radius: 20px;
  padding: 2px 8px;
  display: inline-block;
}

/* ── 종목 카드 ── */
.event-card {
  background: white;
  border-radius: 20px;
  padding: 20px;
  margin-bottom: 16px;
  box-shadow: 0 2px 14px rgba(0,0,0,0.06);
}
.event-header {
  display: flex; align-items: center;
  margin-bottom: 16px;
}
.event-icon {
  width: 42px; height: 42px;
  border-radius: 12px;
  display: flex; align-items: center; justify-content: center;
  font-size: 22px;
  margin-right: 12px; flex-shrink: 0;
}
.event-title { font-size: 15px; font-weight: 700; color: #1a1a2e; }
.event-unit  { font-size: 12px; color: #bbb; margin-top: 2px; }

.stat-row {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: 12px;
}
.best-label  { font-size: 11px; color: #aaa; margin-bottom: 4px; }
.best-record { font-size: 32px; font-weight: 800; color: #1a1a2e; line-height: 1; }
.best-unit   { font-size: 14px; color: #aaa; font-weight: 400; margin-left: 3px; }
.achievement { text-align: right; }
.ach-label   { font-size: 11px; color: #aaa; margin-bottom: 2px; }
.ach-pct     { font-size: 24px; font-weight: 800; }

.progress-wrap {
  background: #f0f0f0; border-radius: 999px;
  height: 8px; margin-bottom: 6px; overflow: hidden;
}
.progress-bar { height: 100%; border-radius: 999px; transition: width 1s ease; }
.progress-meta {
  display: flex; justify-content: space-between;
  font-size: 11px; color: #ccc; margin-bottom: 16px;
}
.chart-wrap { height: 160px; position: relative; }

/* ── 기록표 ── */
.table-wrap { overflow-x: auto; }
table { width: 100%; border-collapse: collapse; font-size: 12px; }
th {
  background: #f8f9ff; color: #555; font-weight: 600;
  padding: 10px 6px; text-align: center;
  border-bottom: 2px solid #e8eaf6; white-space: nowrap;
}
td {
  padding: 10px 6px; text-align: center;
  border-bottom: 1px solid #f0f0f0; color: #333;
}
tr:last-child td { border-bottom: none; }
.official-row td { background: #f0f4ff; font-weight: 700; color: #1a237e; }
.tag-official {
  display: inline-block; background: #1a237e; color: white;
  font-size: 9px; padding: 2px 5px; border-radius: 4px; margin-left: 3px;
}
.tag-monthly {
  display: inline-block; background: #e8eaf6; color: #3949ab;
  font-size: 9px; padding: 2px 5px; border-radius: 4px; margin-left: 3px;
}

/* ── 색상 ── */
.ic1{background:#e8eaf6} .ic2{background:#e8f5e9}
.ic3{background:#fff3e0} .ic4{background:#fce4ec}
.pb1{background:linear-gradient(90deg,#3949ab,#5c6bc0)}
.pb2{background:linear-gradient(90deg,#2e7d32,#43a047)}
.pb3{background:linear-gradient(90deg,#e65100,#fb8c00)}
.pb4{background:linear-gradient(90deg,#880e4f,#e91e63)}
.ap1{color:#3949ab} .ap2{color:#2e7d32}
.ap3{color:#e65100} .ap4{color:#880e4f}

.loading { text-align:center; padding:80px 0; color:#aaa; font-size:14px; }
.tab-content { display: none; }
.tab-content.active { display: block; }
</style>
</head>
<body>

<!-- ══ 메인 페이지 ══ -->
<div id="mainPage">
  <div class="header">
    <h1>🏆 동국대 체교과</h1>
    <p>실기 기록 트래커</p>
  </div>
  <div class="container">
    <div class="section-title">STUDENTS</div>
    <div class="student-grid" id="studentGrid">
      <div class="loading" style="grid-column:1/-1">불러오는 중...</div>
    </div>
  </div>
</div>

<!-- ══ 상세 페이지 ══ -->
<div id="detailPage">
  <div class="detail-header">
    <button class="back-btn" onclick="goBack()">←</button>
    <div class="detail-school" id="dSchool"></div>
    <div class="detail-name"   id="dName"></div>
    <div class="detail-sub">동국대학교 체육교육과</div>
    <div class="detail-badge"  id="dBadge"></div>
  </div>
  <div class="tab-wrap">
    <button class="tab-btn active" onclick="switchTab('chart')">📊 차트</button>
    <button class="tab-btn"        onclick="switchTab('table')">📋 기록표</button>
  </div>
  <div class="container">
    <div class="tab-content active" id="tab-chart">
      <div id="chartArea"></div>
    </div>
    <div class="tab-content" id="tab-table">
      <div id="tableArea"></div>
    </div>
  </div>
</div>

<script>
// ══════════════════════════════
//  설정 (여기만 수정!)
// ══════════════════════════════
const SHEET_ID  = '1-uvH7koGGIEYXO8mL56xVUbUWXEbNPVuVP3htZ2wQMY';
const SHEET_TAB = '기록데이터';

// 만점 기준
const STD = {
  남: {
    strength:{ max:220,  min:130,  unit:'kg', higher:true  },
    flex:    { max:30.0, min:11.9, unit:'cm', higher:true  },
    jump:    { max:300,  min:254,  unit:'cm', higher:true  },
    run:     { max:7.19, min:9.90, unit:'초',  higher:false }
  },
  여: {
    strength:{ max:151,  min:60,   unit:'kg', higher:true  },
    flex:    { max:32.0, min:13.9, unit:'cm', higher:true  },
    jump:    { max:250,  min:199,  unit:'cm', higher:true  },
    run:     { max:7.60, min:10.90,unit:'초',  higher:false }
  }
};

const EVENTS = [
  { key:'strength', col:5,  scoreCol:6,  label:'배근력',              icon:'💪', ci:'1' },
  { key:'flex',     col:7,  scoreCol:8,  label:'앉아 윗몸 앞으로 굽히기', icon:'🧘', ci:'2' },
  { key:'jump',     col:9,  scoreCol:10, label:'제자리 멀리뛰기',      icon:'🦘', ci:'3' },
  { key:'run',      col:11, scoreCol:12, label:'중량메고 달리기',      icon:'🏃', ci:'4' }
];

const COLORS = {
  '1':{ line:'#3949ab', fill:'rgba(57,73,171,0.08)'  },
  '2':{ line:'#2e7d32', fill:'rgba(46,125,50,0.08)'  },
  '3':{ line:'#e65100', fill:'rgba(230,81,0,0.08)'   },
  '4':{ line:'#880e4f', fill:'rgba(136,14,79,0.08)'  }
};

// ══════════════════════════════
//  전역 데이터
// ══════════════════════════════
let allStudents = {};  // { 이름: { gender, school, official:[], monthly:[] } }
let charts = [];

// ══════════════════════════════
//  초기화
// ══════════════════════════════
const CSV_URL = `https://docs.google.com/spreadsheets/d/${SHEET_ID}/gviz/tq?tqx=out:csv&sheet=${encodeURIComponent(SHEET_TAB)}`;

fetch(CSV_URL)
  .then(r => r.text())
  .then(csv => {
    const rows = parseCSV(csv);
    parseAllData(rows);
    renderMainPage();
  })
  .catch(() => {
    document.getElementById('studentGrid').innerHTML =
      '<div class="loading" style="grid-column:1/-1">❌ 데이터를 불러올 수 없어요.<br>시트 공개 설정을 확인해주세요.</div>';
  });

// ══════════════════════════════
//  CSV 파싱
// ══════════════════════════════
function parseCSV(text) {
  return text.trim().split('\n').map(line => {
    const result = []; let cur = '', inQ = false;
    for (let ch of line) {
      if (ch === '"') inQ = !inQ;
      else if (ch === ',' && !inQ) { result.push(cur.trim()); cur = ''; }
      else cur += ch;
    }
    result.push(cur.trim());
    return result;
  });
}

// ══════════════════════════════
//  전체 데이터 파싱
// ══════════════════════════════
function parseAllData(rows) {
  allStudents = {};
  for (let i = 1; i < rows.length; i++) {
    const r = rows[i];
    if (!r[0] || !r[2]) continue;

    const type   = r[0];
    const date   = r[1] || '';
    const name   = r[2];
    const gender = r[3] || '남';
    const school = r[4] || '';

    if (!allStudents[name]) {
      allStudents[name] = { gender, school, official:[], monthly:[] };
    }

    const item = {
      date,
      strength: parseFloat(r[5])  || null,
      strScore: r[6]  || '',
      flex:     parseFloat(r[7])  || null,
      flxScore: r[8]  || '',
      jump:     parseFloat(r[9])  || null,
      jmpScore: r[10] || '',
      run:      r[11] === '미실시' ? null : (parseFloat(r[11]) || null),
      runScore: r[12] || ''
    };

    if (type.includes('공식')) allStudents[name].official.push(item);
    else                       allStudents[name].monthly.push(item);
  }
}

// ══════════════════════════════
//  메인 페이지 렌더링
// ══════════════════════════════
function renderMainPage() {
  const grid = document.getElementById('studentGrid');
  grid.innerHTML = '';

  const names = Object.keys(allStudents);
  if (names.length === 0) {
    grid.innerHTML = '<div class="loading" style="grid-column:1/-1">등록된 학생이 없어요.</div>';
    return;
  }

  names.forEach(name => {
    const s      = allStudents[name];
    const isMale = s.gender === '남';
    const emoji  = isMale ? '🧑' : '👩';
    const aClass = isMale ? 'male-avatar'   : 'female-avatar';
    const cClass = isMale ? 'male-card'     : 'female-card';
    const bClass = isMale ? 'male-badge'    : 'female-badge';
    const bLabel = isMale ? '남' : '여';

    const card = document.createElement('div');
    card.className = `student-card ${cClass}`;
    card.innerHTML = `
      <div class="avatar ${aClass}">${emoji}</div>
      <div class="student-name">${name}</div>
      <div class="student-school">${s.school}</div>
      <span class="gender-badge ${bClass}">${bLabel}</span>`;
    card.onclick = () => openDetail(name);
    grid.appendChild(card);
  });
}

// ══════════════════════════════
//  상세 페이지 열기
// ══════════════════════════════
function openDetail(name) {
  const s = allStudents[name];

  // 헤더 세팅
  document.getElementById('dSchool').textContent = s.school;
  document.getElementById('dName').textContent   = name;
  const badge = document.getElementById('dBadge');
  badge.textContent = s.gender === '남' ? '🧑 남성' : '👩 여성';

  // 탭 초기화
  switchTab('chart');

  // 차트 렌더
  renderChartTab(name, s);
  renderTableTab(s);

  // 페이지 전환
  document.getElementById('mainPage').style.display  = 'none';
  document.getElementById('detailPage').style.display = 'block';
  window.scrollTo(0, 0);
}

// ══════════════════════════════
//  뒤로가기
// ══════════════════════════════
function goBack() {
  // 차트 인스턴스 제거
  charts.forEach(c => c.destroy());
  charts = [];

  document.getElementById('detailPage').style.display = 'none';
  document.getElementById('mainPage').style.display   = 'block';
  window.scrollTo(0, 0);
}

// ══════════════════════════════
//  탭 전환
// ══════════════════════════════
function switchTab(name) {
  document.querySelectorAll('.tab-btn').forEach((b,i) => {
    b.classList.toggle('active', ['chart','table'][i] === name);
  });
  document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
  document.getElementById('tab-' + name).classList.add('active');
}

// ══════════════════════════════
//  차트 탭 렌더링
// ══════════════════════════════
function renderChartTab(name, s) {
  const area = document.getElementById('chartArea');
  area.innerHTML = '';
  charts.forEach(c => c.destroy());
  charts = [];

  const std = STD[s.gender] || STD['남'];

  // 공식테스트 배너
  if (s.official.length > 0) {
    const ov = s.official[s.official.length - 1];
    const banner = document.createElement('div');
    banner.className = 'official-banner';
    banner.innerHTML = `
      <div class="official-title">🏅 공식 테스트 최근 기록</div>
      <div class="official-date">${ov.date}</div>
      <div class="official-grid">
        ${makeOI('💪','배근력',    ov.strength,'kg', ov.strScore)}
        ${makeOI('🧘','좌전굴',    ov.flex,    'cm', ov.flxScore)}
        ${makeOI('🦘','멀리뛰기',  ov.jump,    'cm', ov.jmpScore)}
        ${makeOI('🏃','달리기',    ov.run,     '초',  ov.runScore)}
      </div>`;
    area.appendChild(banner);
  }

  // 월별 차트
  const monthly = [...s.monthly].reverse();
  const labels  = monthly.map(r => r.date);

  EVENTS.forEach(ev => {
    const values = monthly.map(r => r[ev.key]);
    const valid  = values.filter(v => v !== null);
    if (valid.length === 0) return;

    const st   = std[ev.key];
    const best = st.higher ? Math.max(...valid) : Math.min(...valid);
    let pct = st.higher
      ? Math.round((best - st.min) / (st.max - st.min) * 100)
      : Math.round((st.min - best) / (st.min - st.max) * 100);
    pct = Math.max(0, Math.min(100, pct));

    const c    = COLORS[ev.ci];
    const card = document.createElement('div');
    card.className = 'event-card';
    card.innerHTML = `
      <div class="event-header">
        <div class="event-icon ic${ev.ci}">${ev.icon}</div>
        <div>
          <div class="event-title">${ev.label}</div>
          <div class="event-unit">단위: ${st.unit} &nbsp;|&nbsp; 만점: ${st.max}${st.unit}</div>
        </div>
      </div>
      <div class="stat-row">
        <div>
          <div class="best-label">월별 최고기록</div>
          <span class="best-record">${best}</span>
          <span class="best-unit">${st.unit}</span>
        </div>
        <div class="achievement">
          <div class="ach-label">만점 달성률</div>
          <div class="ach-pct ap${ev.ci}">${pct}%</div>
        </div>
      </div>
      <div class="progress-wrap">
        <div class="progress-bar pb${ev.ci}" id="pb_${ev.key}" style="width:0%"></div>
      </div>
      <div class="progress-meta">
        <span>최저 ${st.min}${st.unit}</span>
        <span>만점 ${st.max}${st.unit}</span>
      </div>
      <div class="chart-wrap">
        <canvas id="chart_${ev.key}"></canvas>
      </div>`;
    area.appendChild(card);

    setTimeout(() => {
      document.getElementById('pb_' + ev.key).style.width = pct + '%';
    }, 100);

    const chart = new Chart(document.getElementById('chart_' + ev.key), {
      type: 'line',
      data: {
        labels,
        datasets: [
          {
            label: ev.label,
            data: values,
            borderColor: c.line,
            backgroundColor: c.fill,
            borderWidth: 2.5,
            pointRadius: 5,
            pointBackgroundColor: c.line,
            fill: true, tension: 0.35, spanGaps: true
          },
          {
            label: '만점기준',
            data: Array(labels.length).fill(st.max),
            borderColor: '#ff5252',
            borderWidth: 1.5,
            borderDash: [5,4],
            pointRadius: 0,
            fill: false
          }
        ]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: { legend:{ display:false } },
        scales: {
          x: { grid:{ display:false }, ticks:{ font:{size:11}, color:'#aaa' } },
          y: { grid:{ color:'#f5f5f5' }, ticks:{ font:{size:11}, color:'#aaa' } }
        }
      }
    });
    charts.push(chart);
  });
}

// ══════════════════════════════
//  기록표 탭 렌더링
// ══════════════════════════════
function renderTableTab(s) {
  const area = document.getElementById('tableArea');

  const allRows = [
    ...s.official.map(r => ({...r, isOfficial:true})),
    ...s.monthly
  ].sort((a,b) => b.date.localeCompare(a.date));

  let html = `
    <div class="event-card" style="padding:0;overflow:hidden;">
    <div class="table-wrap"><table>
      <thead><tr>
        <th>날짜</th>
        <th>배근력<br><small style="font-weight:400;color:#aaa">kg</small></th>
        <th>점수</th>
        <th>좌전굴<br><small style="font-weight:400;color:#aaa">cm</small></th>
        <th>점수</th>
        <th>멀리뛰기<br><small style="font-weight:400;color:#aaa">cm</small></th>
        <th>점수</th>
        <th>달리기<br><small style="font-weight:400;color:#aaa">초</small></th>
        <th>점수</th>
      </tr></thead><tbody>`;

  allRows.forEach(r => {
    const cls = r.isOfficial ? 'official-row' : '';
    const tag = r.isOfficial
      ? '<span class="tag-official">공식</span>'
      : '<span class="tag-monthly">연습</span>';
    html += `
      <tr class="${cls}">
        <td style="white-space:nowrap">${r.date}${tag}</td>
        <td>${r.strength ?? '-'}</td>
        <td>${r.strScore || '-'}</td>
        <td>${r.flex     ?? '-'}</td>
        <td>${r.flxScore || '-'}</td>
        <td>${r.jump     ?? '-'}</td>
        <td>${r.jmpScore || '-'}</td>
        <td>${r.run      ?? '미실시'}</td>
        <td>${r.runScore || '-'}</td>
      </tr>`;
  });

  html += `</tbody></table></div></div>`;
  area.innerHTML = html;
}

// ══════════════════════════════
//  헬퍼
// ══════════════════════════════
function makeOI(icon, label, value, unit, score) {
  return `
    <div class="official-item">
      <div class="oi-label">${icon} ${label}</div>
      <div>
        <span class="oi-value">${value ?? '-'}</span>
        <span class="oi-unit">${value ? unit : ''}</span>
      </div>
      ${score ? `<div class="oi-score">점수 ${score}</div>` : ''}
    </div>`;
}
</script>
</body>
</html>
