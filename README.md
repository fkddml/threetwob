<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>투자실험실</title>

  <style>
    :root {
      --paper: #f2f9fc;
      --white: #fff;
      --ink: #18345a;
      --blue: #277fc4;
      --sky: #bfe8f5;
      --line: #18345a;
      --muted: #62758a;
      --up: #18734e;
      --down: #c14f5c;
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      color: var(--ink);
      background:
        radial-gradient(#dcebf1 0.8px, transparent 0.8px) 0 0 / 17px 17px,
        var(--paper);
      font-family: "Apple SD Gothic Neo", "Malgun Gothic", Arial, sans-serif;
      letter-spacing: -0.03em;
    }

    button, textarea { font: inherit; }
    button { color: inherit; cursor: pointer; }

    header {
      position: sticky;
      top: 0;
      z-index: 5;
      display: flex;
      justify-content: space-between;
      align-items: center;
      min-height: 72px;
      padding: 10px max(20px, calc((100vw - 1100px) / 2));
      background: rgba(242, 249, 252, 0.96);
      border-bottom: 2px solid var(--line);
    }

    .home-button, .menu-button {
      min-height: 52px;
      padding: 0 18px;
      border: 2px solid var(--line);
      background: var(--white);
      font-weight: 800;
    }

    main {
      width: min(100% - 36px, 980px);
      min-height: calc(100dvh - 132px);
      margin: 0 auto;
      padding: 44px 0 60px;
    }

    footer {
      padding: 18px max(20px, calc((100vw - 1100px) / 2));
      color: var(--white);
      background: var(--ink);
      font-size: 14px;
    }

    h1, h2, p { margin-top: 0; }
    h1 { font-size: clamp(36px, 7vw, 64px); line-height: 1.05; }
    h2 { font-size: clamp(22px, 4vw, 32px); }
    p, li { line-height: 1.65; }

    .eyebrow {
      margin-bottom: 12px;
      color: var(--blue);
      font-size: 14px;
      font-weight: 900;
      letter-spacing: 0.12em;
    }

    .lead { font-size: clamp(18px, 3vw, 23px); }
    .muted { color: var(--muted); }
    .panel {
      margin: 18px 0;
      padding: 22px;
      border: 2px solid var(--line);
      background: var(--white);
      box-shadow: 4px 4px 0 var(--sky);
    }

    .primary, .secondary, .choice, .step {
      min-height: 56px;
      padding: 12px 18px;
      border: 2px solid var(--line);
      background: var(--white);
      font-weight: 800;
    }

    .primary {
      width: 100%;
      min-height: 76px;
      color: var(--white);
      background: var(--ink);
      box-shadow: 4px 4px 0 var(--blue);
      font-size: 21px;
    }

    .secondary { background: var(--sky); }
    .primary:disabled { opacity: 0.45; cursor: not-allowed; }
    .grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 14px; }
    .company h2 { margin-bottom: 4px; font-size: 25px; }
    .company p { margin-bottom: 8px; }
    .company .hint { color: var(--blue); font-weight: 800; }

    .steps { display: flex; gap: 8px; flex-wrap: wrap; }
    .step.active { color: var(--white); background: var(--blue); }

    .reasons { display: flex; gap: 9px; flex-wrap: wrap; }
    .choice.selected { background: var(--sky); box-shadow: 3px 3px 0 var(--blue); }

    .weight-row { display: flex; align-items: center; gap: 8px; }
    .weight-row button { min-width: 58px; min-height: 46px; }
    .weight-value { min-width: 48px; text-align: center; font-weight: 900; }

    .summary {
      display: flex;
      justify-content: space-between;
      gap: 12px;
      flex-wrap: wrap;
      font-size: 20px;
      font-weight: 900;
    }

    .up { color: var(--up); }
    .down { color: var(--down); }
    .two-col { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
    .type-card { border-left: 6px solid var(--blue); }
    textarea {
      width: 100%;
      min-height: 260px;
      padding: 16px;
      border: 2px solid var(--line);
      background: var(--white);
      color: var(--ink);
      line-height: 1.65;
    }

    .menu {
      display: flex;
      gap: 8px;
      margin: 0 auto;
      padding: 10px;
      border: 2px solid var(--line);
      background: var(--white);
    }

    .menu[hidden] { display: none; }
    .menu-wrap { display: flex; align-items: center; gap: 10px; }
    .menu button { min-height: 46px; }
    .luck-dot {
      display: inline-block;
      width: 30px;
      height: 30px;
      border: 1px solid #789;
      border-radius: 50%;
      vertical-align: middle;
    }

    @media (max-width: 650px) {
      header { padding: 8px 12px; }
      main { width: min(100% - 24px, 980px); padding-top: 28px; }
      .grid, .two-col { grid-template-columns: 1fr; }
      .panel { padding: 17px; }
      .menu-wrap { gap: 6px; }
      .menu { position: absolute; top: 66px; right: 12px; flex-direction: column; }
    }
  </style>
</head>

<body>
  <header>
    <button class="home-button" data-action="route" data-route="player" aria-label="학생 화면">⌂</button>
    <div class="menu-wrap">
      <nav id="menu" class="menu" hidden>
        <button class="secondary" data-action="route" data-route="player">학생 참여</button>
        <button class="secondary" data-action="route" data-route="teacher">교육자 자료</button>
      </nav>
      <button class="menu-button" data-action="menu">☰ 메뉴</button>
    </div>
  </header>

  <main id="app"></main>

  <footer>
    가상 시뮬레이션이에요. 실제 돈·실제 회사가 아니며 투자 조언이 아니에요.
    개인 기록은 이 기기에 저장돼요.
  </footer>

  <script>
    const KEY = "investment-lab-single-html";
    const REPORT_KEY = KEY + "-report";
    const START_CASH = 1000000;
    const REASONS = ["매출·비용 비교", "업종 나눠 담기", "현금 남기기", "인기 참고"];

    const passes = [
      {
        companies: [
          [
            ["비트엔터", "엔터", "아이돌 콘서트·공연 기획"],
            ["스테이지뮤직", "엔터", "아티스트 공연·투어"],
            ["팬메이트", "팬 플랫폼", "아티스트 소통 서비스"],
            ["플레이사운드", "음악", "음원 스트리밍 서비스"]
          ],
          [
            ["스윗컵", "카페", "커피·시즌 음료 판매"],
            ["도어딜리버리", "배달", "음식 배달 플랫폼"],
            ["포켓스토어", "편의점", "간식·간편식 판매"],
            ["슈가링", "디저트", "도넛·디저트 매장"]
          ],
          [
            ["블룸코스", "뷰티", "스킨케어 제품"],
            ["틴트랩", "메이크업", "색조 화장품"],
            ["무드아이", "패션 소품", "안경·패션 팝업"],
            ["픽셀모바일", "기기", "스마트폰·모바일 기기"]
          ],
          [
            ["클로젯패션", "패션", "온라인 패션·브랜드 협업"],
            ["필름온", "영상", "영화·시리즈 스트리밍"],
            ["포토플레이", "사진", "셀프 사진 스튜디오"],
            ["페이지툰", "웹툰", "웹툰·영상화 콘텐츠"]
          ]
        ],
        rounds: [
          {
            title: "1군 아이돌 콘서트 공지!",
            headline: "관심이 실제 매출과 이익으로 이어질까요?",
            hints: ["티켓 판매 기대 · 무대 제작비도 증가", "추가 회차 공지 · 공연장 규모 확대", "팬클럽 가입 문의 증가", "컴백 음원 기대 · 할인 경쟁 우려"],
            outcome: "티켓 판매가 늘었어요. 다만 제작비와 할인 경쟁에 따라 회사별 이익은 달랐어요."
          },
          {
            title: "간식 예산이 줄었어요",
            headline: "물가가 올라 외식·배달 지출을 줄이는 사람이 늘었어요.",
            hints: ["시즌 음료 주문 감소", "배달비 부담에 주문 감소", "저렴한 도시락 판매 증가", "재료비 상승 · 디저트 구매 감소"],
            outcome: "소비가 줄어도 회사마다 판매량과 비용이 달라 결과가 달랐어요."
          },
          {
            title: "화제의 신상, 진짜 잘 팔릴까?",
            headline: "조회 수뿐 아니라 주문과 비용도 살펴보세요.",
            hints: ["스킨케어 주문 소폭 증가", "새 틴트 재주문 증가", "팝업은 인기 · 운영비 부담", "새 기기 예약 호조"],
            outcome: "관심이 주문으로 이어진 상품도 있지만, 행사 비용이 커 이익이 적은 곳도 있어요."
          },
          {
            title: "기다리던 콘텐츠 공개",
            headline: "새 콘텐츠와 협업 상품이 매출로 이어질까요?",
            hints: ["할인 경쟁으로 이익 감소 우려", "새 시리즈 제작비 증가", "사진 프레임 협업 인기", "웹툰 영상화 일정 확정"],
            outcome: "관심도 중요하지만 제작비와 판매 성과도 결과를 갈랐어요."
          }
        ],
        rates: [
          [0.12, 0.04, 0.02, -0.06],
          [-0.15, -0.08, 0.03, -0.12],
          [0.04, 0.18, -0.02, 0.06],
          [-0.06, -0.04, 0.05, -0.20]
        ]
      },
      {
        companies: [
          [
            ["모빌온", "모빌리티", "전기 자전거·공유 이동"],
            ["플라이패스", "교통", "광역 교통 정기권"],
            ["루트트립", "여행", "국내 소도시 여행"],
            ["스테이브릿지", "숙박", "도심형 게스트하우스"]
          ],
          [
            ["픽셀스터디", "교육", "온라인 과외·학습 콘텐츠"],
            ["에듀노트", "학습 도구", "디지털 플래너·노트"],
            ["퀴즈팜", "교육 앱", "문제 풀이 구독 서비스"],
            ["캠프랩", "교육 행사", "진로·학습 캠프"]
          ],
          [
            ["런웨이즈", "스포츠", "러닝화·운동복"],
            ["핏데이", "운동", "홈트레이닝 구독 서비스"],
            ["플레이볼", "스포츠 용품", "팀 유니폼·공 용품"],
            ["아웃룸", "아웃도어", "캠핑 장비 대여"]
          ],
          [
            ["리필스테이션", "친환경", "세제·생활용품 리필숍"],
            ["그린보틀", "생활용품", "다회용 물병·용기"],
            ["새벽바구니", "식품", "친환경 식재료 배송"],
            ["플랜트키친", "식품", "식물성 간편식"]
          ]
        ],
        rounds: [
          {
            title: "주말 교통비 할인",
            headline: "주말 교통 할인으로 근교 나들이가 늘었어요.",
            signals: [[18, 7], [9, 6], [20, 24], [12, 8]],
            outcome: "매출 변화에서 비용 변화를 뺀 차이가 주가 결과에 반영됐어요."
          },
          {
            title: "시험 대비 학습 수요",
            headline: "모의고사를 앞두고 학습 도구와 강의 구독이 늘었어요.",
            signals: [[24, 8], [12, 6], [21, 25], [16, 24]],
            outcome: "판매가 늘어도 콘텐츠·행사 비용까지 함께 오르면 결과는 달라져요."
          },
          {
            title: "학교 러닝 챌린지",
            headline: "학생들이 참여하는 러닝 행사가 열렸어요.",
            signals: [[15, 9], [20, 10], [18, 26], [11, 9]],
            outcome: "참여 인기가 높아도 운영·물류 비용이 더 커지면 이익은 줄 수 있어요."
          },
          {
            title: "다회용품 할인 주간",
            headline: "학교와 동네에서 다회용품 할인 행사가 시작됐어요.",
            signals: [[17, 5], [10, 4], [15, 23], [12, 8]],
            outcome: "행사 인기도 살피되 실제 매출과 비용 차이를 함께 봐요."
          }
        ]
      }
    ];

    const COLORS = [
      ["쿨 블루", "#DCEEFF"],
      ["라일락", "#E8E1FF"],
      ["버터 옐로", "#FFF0B5"],
      ["민트", "#D6F3E6"],
      ["코랄", "#FFD9D1"],
      ["베리 핑크", "#F4DCEF"],
      ["아이스 그레이", "#E6EDF5"]
    ];

    function safeGet(key) {
      try { return localStorage.getItem(key); }
      catch { return null; }
    }

    function safeSet(key, value) {
      try { localStorage.setItem(key, value); }
      catch { /* 브라우저에서 저장을 허용하지 않으면 열린 동안만 진행합니다. */ }
    }

    function loadGame() {
      try { return JSON.parse(safeGet(KEY) || "null"); }
      catch { return null; }
    }

    let game = loadGame();
    let pick = { weights: [0, 0, 0, 0], reason: "" };

    function saveGame() {
      if (game) safeSet(KEY, JSON.stringify(game));
      else {
        try { localStorage.removeItem(KEY); }
        catch {}
      }
    }

    function money(value) {
      return Math.round(value).toLocaleString("ko-KR") + "원";
    }

    function companyRate(pass, round, index) {
      if (pass === 0) return passes[0].rates[round][index];
      const [sales, cost] = passes[1].rounds[round].signals[index];
      return (sales - cost) / 200;
    }

    function begin() {
      game = { stage: "play", pass: 0, round: 0, cash: START_CASH, records: [] };
      pick = { weights: [0, 0, 0, 0], reason: "" };
      saveGame();
      render();
    }

    function invest() {
      if (!game || !pick.reason) return;

      const companies = passes[game.pass].companies[game.round];
      const rates = companies.map((_, i) => companyRate(game.pass, game.round, i));
      const before = game.cash;
      let after = before;

      pick.weights.forEach((weight, i) => {
        const amount = Math.floor(before * weight / 100);
        after += Math.round(amount * rates[i]);
      });

      game.cash = after;
      game.records.push({
        pass: game.pass + 1,
        round: game.round + 1,
        cashIn: before,
        cashOut: after,
        names: companies.map(company => company[0]),
        weights: [...pick.weights],
        rates,
        reason: pick.reason
      });
      game.stage = "reveal";
      pick = { weights: [0, 0, 0, 0], reason: "" };
      saveGame();
      render();
    }

    function next() {
      if (game.round < 3) {
        game.round++;
        game.stage = "play";
      } else if (game.pass === 0) {
        game.stage = "teach";
      } else {
        game.stage = "done";
        game.luckyColor = COLORS[Math.floor(Math.random() * COLORS.length)];
      }
      saveGame();
      render();
    }

    function continueAfterLesson() {
      game = {
        ...game,
        stage: "play",
        pass: 1,
        round: 0,
        cash: START_CASH
      };
      pick = { weights: [0, 0, 0, 0], reason: "" };
      saveGame();
      render();
    }

    function analyze(records) {
      const first = records.filter(row => row.pass === 1);
      const second = records.filter(row => row.pass === 2);
      const count = (rows, reason) => rows.filter(row => row.reason === reason).length;
      const concentrated = records.filter(row => Math.max(...row.weights) >= 75).length;
      const avgCash = records.reduce((sum, row) =>
        sum + 100 - row.weights.reduce((a, b) => a + b, 0), 0) / records.length;
      const spreadCount = records.filter(row =>
        row.reason === "업종 나눠 담기").length;
      const numberBefore = count(first, "매출·비용 비교");
      const numberAfter = count(second, "매출·비용 비교");
      const reasonVariety = new Set(records.map(row => row.reason)).size;

      if (concentrated >= 3) {
        return ["한 종목에 꽂힌 집중형", "확신이 생기면 과감하게 선택하는 추진력이 있어요.", "한 회사에 몰리면 작은 뉴스에도 크게 흔들려요. 다음엔 두 곳 이상에 나눠 봐요."];
      }
      if (numberAfter - numberBefore >= 2) {
        return ["배움을 바로 쓰는 업그레이더", "②에서 매출·비용을 따져본 선택이 늘었어요.", "숫자를 읽은 다음, 비용이 더 빠르게 늘지는 않는지도 확인해 보세요."];
      }
      if (spreadCount >= 3 && avgCash < 15) {
        return ["전액 분산하는 올인형", "여러 회사를 골라 한 곳에 몰리는 위험을 낮춰요.", "전부 투자하면 조정할 여지가 없어요. 일부 현금도 남겨 보세요."];
      }
      if (spreadCount >= 3) {
        return ["골고루 담는 분산 설계자", "한 곳에만 기대지 않고 선택지를 나누는 편이에요.", "회사 수뿐 아니라 업종도 다른지 살펴보면 더 좋아요."];
      }
      if (count(records, "현금 남기기") >= 3 || avgCash >= 32) {
        return ["현금을 챙기는 안정 추구형", "확신이 없을 땐 투자하지 않는 선택도 할 줄 알아요.", "현금은 안전하지만 수익도 없어요. 기회와 안전 사이의 비중을 비교해 보세요."];
      }
      if (count(records, "인기 참고") >= 3) {
        return ["유행을 빨리 읽는 트렌드 캐처", "사람들의 관심이 어디로 가는지 잘 포착해요.", "관심이 매출로 이어지는지, 비용까지 빼도 이익인지 확인해 보세요."];
      }
      if (count(records, "매출·비용 비교") >= 3) {
        return ["숫자를 읽는 꼼꼼 분석가", "화제성보다 매출과 비용을 근거로 선택하는 편이에요.", "좋은 숫자도 한 회사에 몰아 담기보다 여러 선택과 비교해 보세요."];
      }
      if (avgCash < 15) {
        return ["기회를 놓치지 않는 실행형", "생각한 선택을 빠르게 투자로 옮기는 편이에요.", "투자 전 매출·비용 근거를 한 번 더 보고, 현금 여지도 남겨 보세요."];
      }
      if (reasonVariety >= 3) {
        return ["상황 따라 바꾸는 유연 탐험가", "한 가지 기준만 고집하지 않고 여러 방법을 시도해요.", "선택 이유를 먼저 정한 뒤, 결과와 비교하면 나만의 기준이 보여요."];
      }
      return ["균형을 찾아가는 밸런서", "투자와 현금, 여러 선택 사이에서 균형을 찾아가고 있어요.", "이번에 가장 효과 있었던 선택 이유를 다음 결정에도 활용해 보세요."];
    }

    function reportText() {
      const first = game.records.filter(row => row.pass === 1);
      const second = game.records.filter(row => row.pass === 2);
      const end1 = first.at(-1)?.cashOut ?? START_CASH;
      const end2 = second.at(-1)?.cashOut ?? START_CASH;
      const type = analyze(game.records);

      return [
        "개인 모의 투자 탐구 기록",
        "① 4라운드 → 투자 기준 설명 → ② 4라운드",
        `① 최종 금액: ${money(end1)}`,
        `② 최종 금액: ${money(end2)}`,
        `최종 금액 변화: ${money(end2 - end1)}`,
        `나의 투자 유형: ${type[0]}`,
        type[1],
        type[2],
        `오늘의 행운 색: ${game.luckyColor.name}`,
        "",
        "선택 이유:",
        ...game.records.map(row => `${row.pass === 1 ? "①" : "②"} ${row.round}라운드 ${row.reason}`),
        "",
        "해석: ②에서는 새로운 회사와 사건, 매출·비용 단서를 사용했어요. 두 세트의 조건이 다르므로 최종 금액 차이만으로 교육의 인과 효과를 단정할 수는 없어요."
      ].join("\n");
    }

    function teacherPage() {
      return `
        <p class="eyebrow">TEACHER</p>
        <h1>교육자 자료</h1>
        <p class="lead">두 게임 사이에 투자 판단 기준을 짧게 이야기해 주세요.</p>

        <section class="panel">
          <h2>진행 순서</h2>
          <p>① 학생이 4라운드 투자</p>
          <p>설명 — 아래 내용을 2~3분 동안 안내</p>
          <p>② 새 가상 100만원으로 4라운드 투자</p>
          <p>결과 비교와 보고서 작성</p>
        </section>

        <section class="panel">
          <h2>1. 뉴스 → 매출과 비용 → 이익</h2>
          <p>좋은 뉴스가 곧 좋은 이익은 아니에요. 매출과 비용을 둘 다 봐야 해요.</p>
          <p><b>② 게임에 바로 적용돼요.</b> 매출 변화율에서 비용 변화율을 빼고 2로 나누면 모의 주가 변화율이에요.</p>
          <p><b>예: 매출 +24%, 비용 +8% → (24−8)÷2 = 주가 +8%</b></p>
          <p>“뉴스를 보면 매출과 비용 중 뭐가 더 크게 변할지 생각해 보자.”</p>
        </section>

        <section class="panel">
          <h2>2. 인기 ≠ 이익</h2>
          <p>모두가 이야기하는 회사라고 돈을 더 버는 건 아니에요. 관심이 실제 매출로 이어졌는지 살펴봐요.</p>
        </section>

        <section class="panel">
          <h2>3. 여러 곳에 나눠 투자하기</h2>
          <p>네 회사에 나눠도 같은 업종이면 같은 뉴스에 함께 오르내릴 수 있어요. 서로 다른 업종인지도 확인해요.</p>
        </section>

        <section class="panel">
          <h2>4. 현금도 선택이에요</h2>
          <p>확신이 없으면 일부를 현금으로 남겨도 돼요. 현금은 주가가 오르지 않지만, 투자 손실도 생기지 않아요.</p>
        </section>

        <section class="panel">
          <h2>5. 결과를 해석할 때</h2>
          <p>두 게임은 회사와 사건이 달라요. 선택 이유와 투자 습관의 변화는 살펴볼 수 있지만, 금액 차이만으로 교육 효과를 단정하지 않아요.</p>
        </section>
      `;
    }

    function render() {
      const app = document.getElementById("app");
      const route = location.hash.replace("#", "") || "player";

      if (route === "teacher") {
        app.innerHTML = teacherPage();
        return;
      }

      if (!game) {
        app.innerHTML = `
          <p class="eyebrow">INVESTMENT EXPERIMENT</p>
          <h1>나의 투자 실험</h1>
          <p class="lead">라운드마다 다른 회사에 투자하고 결과를 확인해요.</p>
          <p class="muted">① 4라운드 · 설명 듣기 · ② 4라운드</p>
          <button class="primary" data-action="start">① 시작</button>
        `;
        return;
      }

      if (game.stage === "teach") {
        app.innerHTML = `
          <p class="eyebrow">LEARN</p>
          <h1>이제 설명을 들어요.</h1>
          <button class="primary" data-action="lesson-next">②로 넘어가기</button>
        `;
        return;
      }

      if (game.stage === "reveal") {
        const row = game.records.at(-1);
        app.innerHTML = `
          <p class="eyebrow">${row.pass === 1 ? "①" : "②"} · ${row.round}/4</p>
          <h1>이번 라운드 결과</h1>
          <p class="lead">${passes[row.pass - 1].rounds[row.round - 1].outcome}</p>
          <section class="panel">
            <div class="summary">
              <span>${money(row.cashOut)}</span>
              <span class="${row.cashOut >= row.cashIn ? "up" : "down"}">
                ${row.cashOut >= row.cashIn ? "+" : ""}${((row.cashOut / row.cashIn - 1) * 100).toFixed(1)}%
              </span>
            </div>
            <ul>
              ${row.names.map((name, i) => `
                <li>${name} · ${row.weights[i]}% ·
                  <b class="${row.rates[i] >= 0 ? "up" : "down"}">${row.rates[i] >= 0 ? "+" : ""}${(row.rates[i] * 100).toFixed(1)}%</b>
                </li>
              `).join("")}
            </ul>
          </section>
          <button class="primary" data-action="next">
            ${row.round === 4 && row.pass === 1 ? "설명 단계로" : row.round === 4 ? "비교 보기" : "다음 라운드"}
          </button>
        `;
        return;
      }

      if (game.stage === "done") {
        const first = game.records.filter(row => row.pass === 1);
        const second = game.records.filter(row => row.pass === 2);
        const type = analyze(game.records);
        const report = safeGet(REPORT_KEY) || reportText();

        app.innerHTML = `
          <p class="eyebrow">RESULT</p>
          <h1>결과 비교</h1>
          <div class="two-col">
            <section class="panel">
              <h2>①</h2>
              <p class="lead">${money(first.at(-1).cashOut)}</p>
              <p>매출·비용 비교 선택: ${first.filter(r => r.reason === "매출·비용 비교").length}/4</p>
            </section>
            <section class="panel">
              <h2>②</h2>
              <p class="lead">${money(second.at(-1).cashOut)}</p>
              <p>매출·비용 비교 선택: ${second.filter(r => r.reason === "매출·비용 비교").length}/4</p>
            </section>
          </div>

          <section class="panel type-card">
            <p class="eyebrow">투자 패턴 · 재미로 보는 유형</p>
            <h2>${type[0]}</h2>
            <p><b>강점</b> · ${type[1]}</p>
            <p><b>다음 팁</b> · ${type[2]}</p>
            <p><b>오늘의 행운 색</b> · ${game.luckyColor.name}
              <span class="luck-dot" style="background:${game.luckyColor.hex}"></span>
            </p>
            <p class="muted">선택 기록으로 만든 규칙 기반 분석이에요. 행운 색은 재미 요소예요.</p>
          </section>

          <h2>탐구 보고서 초안</h2>
          <textarea id="report">${escapeHtml(report)}</textarea>
          <p>
            <button class="secondary" data-action="download">보고서 TXT</button>
            <button class="secondary" data-action="reset">새로 하기</button>
          </p>
        `;
        return;
      }

      const pass = passes[game.pass];
      const companies = pass.companies[game.round];
      const event = pass.rounds[game.round];
      const invested = pick.weights.reduce((a, b) => a + b, 0);

      app.innerHTML = `
        <p class="eyebrow">${game.pass === 0 ? "①" : "②"} · ${game.round + 1}/4</p>
        <h1>${event.title}</h1>
        <p class="lead">${event.headline}</p>
        ${game.pass === 1 ? `<p><b>매출 변화와 비용 변화를 비교해 보세요.</b></p>` : ""}
        <p class="summary">
          <span>투자 가능 ${money(game.cash)}</span>
          <span>현금 ${100 - invested}%</span>
        </p>

        <div class="grid">
          ${companies.map((company, i) => {
            const weight = pick.weights[i];
            const hint = game.pass === 0
              ? event.hints[i]
              : `매출 +${event.signals[i][0]}% · 비용 +${event.signals[i][1]}%`;
            return `
              <article class="panel company">
                <p class="eyebrow">${company[1]}</p>
                <h2>${company[0]}</h2>
                <p>${company[2]}</p>
                <p class="hint">${hint}</p>
                <div class="weight-row">
                  <button class="secondary" data-action="weight" data-index="${i}" data-delta="-25">−25%</button>
                  <span class="weight-value">${weight}%</span>
                  <button class="secondary" data-action="weight" data-index="${i}" data-delta="25">+25%</button>
                </div>
              </article>
            `;
          }).join("")}
        </div>

        <section class="panel">
          <h2>선택 이유</h2>
          <div class="reasons">
            ${REASONS.map(reason => `
              <button class="choice ${pick.reason === reason ? "selected" : ""}"
                data-action="reason" data-reason="${reason}">${reason}</button>
            `).join("")}
          </div>
        </section>

        <button class="primary" data-action="invest" ${pick.reason ? "" : "disabled"}>
          ${game.pass === 1 && game.round === 3 ? "마치고 비교 보기" : "라운드 확정"}
        </button>
      `;
    }

    function escapeHtml(text) {
      return String(text).replace(/[&<>"']/g, char => ({
        "&": "&amp;", "<": "&lt;", ">": "&gt;", '"': "&quot;", "'": "&#39;"
      })[char]);
    }

    document.addEventListener("click", event => {
      const button = event.target.closest("[data-action]");
      if (!button) return;

      const action = button.dataset.action;

      if (action === "menu") {
        const menu = document.getElementById("menu");
        menu.hidden = !menu.hidden;
      }
      if (action === "route") {
        location.hash = button.dataset.route;
        document.getElementById("menu").hidden = true;
      }
      if (action === "start") begin();
      if (action === "invest") invest();
      if (action === "next") next();
      if (action === "lesson-next") continueAfterLesson();

      if (action === "reason") {
        pick.reason = button.dataset.reason;
        render();
      }

      if (action === "weight") {
        const index = Number(button.dataset.index);
        const delta = Number(button.dataset.delta);
        const nextWeight = Math.max(0, Math.min(100, pick.weights[index] + delta));
        const total = pick.weights.reduce((a, b) => a + b, 0) - pick.weights[index] + nextWeight;

        if (total <= 100) {
          pick.weights[index] = nextWeight;
          render();
        }
      }

      if (action === "download") {
        const text = document.getElementById("report").value;
        const link = document.createElement("a");
        link.href = URL.createObjectURL(new Blob([text], { type: "text/plain;charset=utf-8" }));
        link.download = "두판_투자탐구.txt";
        link.click();
        URL.revokeObjectURL(link.href);
      }

      if (action === "reset" && confirm("기록을 지우고 새로 시작할까요?")) {
        game = null;
        pick = { weights: [0, 0, 0, 0], reason: "" };
        safeSet(REPORT_KEY, "");
        saveGame();
        render();
      }
    });

    document.addEventListener("input", event => {
      if (event.target.id === "report") safeSet(REPORT_KEY, event.target.value);
    });

    window.addEventListener("hashchange", render);
    render();
  </script>
</body>
</html>
