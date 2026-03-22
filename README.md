<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CPC Commission Calculator | Yelp Ads</title>
<meta name="description" content="Quick commission calculator for Yelp Ads reps—calculate CPC points on the fly">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  body { 
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; 
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: #1a1a1a; 
    min-height: 100vh; 
    display: flex; 
    align-items: center; 
    justify-content: center; 
    padding: 1rem; 
  }
  .widget { 
    background: #ffffff; 
    border-radius: 20px; 
    box-shadow: 0 20px 60px rgba(0,0,0,0.3);
    padding: 2rem 1.5rem; 
    width: 100%; 
    max-width: 420px; 
  }
  .header { 
    text-align: center; 
    margin-bottom: 1.5rem; 
    padding-bottom: 1rem; 
    border-bottom: 1px solid rgba(0,0,0,0.08); 
  }
  .header h1 { 
    font-size: 22px; 
    font-weight: 600; 
    color: #1a1a1a; 
    margin-bottom: 4px;
  }
  .header p { 
    font-size: 13px; 
    color: #888; 
  }
  
  .input-group { margin-bottom: 1.25rem; }
  .input-group label { 
    display: block; 
    font-size: 12px; 
    font-weight: 500; 
    color: #666; 
    margin-bottom: 6px; 
    text-transform: uppercase;
    letter-spacing: 0.03em;
  }
  select { 
    width: 100%;
    height: 44px; 
    padding: 0 12px; 
    border: 1.5px solid rgba(0,0,0,0.12); 
    border-radius: 10px; 
    font-size: 15px; 
    background: #fff; 
    color: #1a1a1a; 
    outline: none; 
    cursor: pointer; 
    transition: all 0.2s;
  }
  select:hover { border-color: #667eea; }
  select:focus { border-color: #667eea; box-shadow: 0 0 0 3px rgba(102,126,234,0.1); }
  
  .toggle-group { margin-bottom: 1.5rem; }
  .toggle-group label { 
    display: block; 
    font-size: 12px; 
    font-weight: 500; 
    color: #666; 
    margin-bottom: 8px; 
    text-transform: uppercase;
    letter-spacing: 0.03em;
  }
  .toggle-pill { 
    display: flex; 
    border: 1.5px solid rgba(0,0,0,0.12); 
    border-radius: 10px; 
    overflow: hidden; 
    background: #f8f8f8;
  }
  .toggle-pill button { 
    flex: 1;
    padding: 10px 16px; 
    font-size: 14px; 
    font-weight: 500;
    background: transparent; 
    border: none; 
    color: #888; 
    cursor: pointer; 
    transition: all 0.2s; 
  }
  .toggle-pill button.active { 
    background: #667eea; 
    color: #fff; 
  }
  
  .result-box { 
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    border-radius: 14px; 
    padding: 1.5rem; 
    margin: 1.5rem 0;
    text-align: center;
  }
  .result-label { 
    font-size: 11px; 
    color: rgba(255,255,255,0.8); 
    margin-bottom: 8px; 
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }
  .result-value { 
    font-size: 36px; 
    font-weight: 700; 
    color: #fff; 
    line-height: 1;
  }
  
  .breakdown { 
    display: grid; 
    grid-template-columns: 1fr 1fr; 
    gap: 10px; 
    margin-bottom: 1.5rem;
  }
  .breakdown-item { 
    background: #f8f8f8; 
    border-radius: 10px; 
    padding: 12px; 
    text-align: center;
  }
  .breakdown-label { 
    font-size: 10px; 
    color: #888; 
    margin-bottom: 4px; 
    text-transform: uppercase;
    letter-spacing: 0.04em;
  }
  .breakdown-value { 
    font-size: 18px; 
    font-weight: 600; 
    color: #1a1a1a; 
  }
  .breakdown-value.blue { color: #667eea; }
  .breakdown-value.green { color: #2d6a1f; }
  .breakdown-value.muted { color: #ccc; }
  
  .share-bar { 
    display: flex; 
    gap: 8px; 
    margin-top: 1.5rem; 
    padding-top: 1.5rem; 
    border-top: 1px solid rgba(0,0,0,0.08);
  }
  .share-btn { 
    flex: 1;
    padding: 12px; 
    border: none; 
    border-radius: 10px; 
    font-size: 13px; 
    font-weight: 600; 
    cursor: pointer; 
    transition: all 0.2s;
  }
  .share-btn.copy { 
    background: #f0f0f0; 
    color: #1a1a1a; 
  }
  .share-btn.copy:hover { background: #e0e0e0; }
  .share-btn.copy.copied { background: #2d6a1f; color: #fff; }
  .share-btn.reset { 
    background: transparent; 
    color: #888; 
    border: 1.5px solid rgba(0,0,0,0.12);
  }
  .share-btn.reset:hover { border-color: #667eea; color: #667eea; }
  
  .footer { 
    text-align: center; 
    margin-top: 1rem; 
    font-size: 11px; 
    color: #aaa; 
  }

  @media (max-width: 480px) {
    .widget { padding: 1.5rem 1.25rem; }
    .result-value { font-size: 32px; }
  }
</style>
</head>
<body>
<div class="widget">
  <div class="header">
    <h1>CPC Commission Calc</h1>
    <p>Quick points for Yelp Ads packages</p>
  </div>
  
  <div class="input-group">
    <label>Daily CPC Budget</label>
    <select id="daily" onchange="calc()">
      <option value="5">$5 / day</option>
      <option value="10">$10 / day</option>
      <option value="15">$15 / day</option>
      <option value="24">$24 / day</option>
      <option value="30">$30 / day</option>
    </select>
  </div>
  
  <div class="input-group">
    <label>Page Upgrade Tier</label>
    <select id="tier" onchange="calc()">
      <option value="none">No upgrade</option>
      <option value="up">Page Upgrade</option>
      <option value="upvl">UP + Verified License</option>
    </select>
  </div>
  
  <div class="toggle-group">
    <label>$300 UFC Credit</label>
    <div class="toggle-pill">
      <button id="ufc-no" class="active" onclick="setUFC(false)">Not included</button>
      <button id="ufc-yes" onclick="setUFC(true)">Included</button>
    </div>
  </div>
  
  <div class="result-box">
    <div class="result-label">Total Commission Points</div>
    <div class="result-value" id="total-out">1.725</div>
  </div>
  
  <div class="breakdown">
    <div class="breakdown-item">
      <div class="breakdown-label">Monthly Spend</div>
      <div class="breakdown-value" id="monthly-out">$300</div>
    </div>
    <div class="breakdown-item">
      <div class="breakdown-label">CPC Points</div>
      <div class="breakdown-value blue" id="cpc-out">1.725</div>
    </div>
    <div class="breakdown-item">
      <div class="breakdown-label">UFC Points</div>
      <div class="breakdown-value muted" id="ufc-out">—</div>
    </div>
    <div class="breakdown-item">
      <div class="breakdown-label">Package Value</div>
      <div class="breakdown-value green" id="package-out">$300</div>
    </div>
  </div>
  
  <div class="share-bar">
    <button class="share-btn copy" id="copy-btn" onclick="copyLink()">📋 Copy Link</button>
    <button class="share-btn reset" onclick="resetCalc()">↺ Reset</button>
  </div>
  
  <div class="footer">
    Yelp Ads Commission Tool
  </div>
</div>

<script>
const DATA = [
  { daily: 5,  monthly: 150, cpc: { none: 0.863, up: 1.553, upvl: 1.725 }, ufc: { none: 0.26, up: 0.41, upvl: 0.45 } },
  { daily: 10, monthly: 300, cpc: { none: 1.725, up: 2.415, upvl: 2.58  }, ufc: { none: 0.45, up: 0.63, upvl: 0.68 } },
  { daily: 15, monthly: 450, cpc: { none: 2.588, up: 3.278, upvl: 3.45  }, ufc: { none: 0.45, up: 0.63, upvl: 0.68 } },
  { daily: 24, monthly: 720, cpc: { none: 3.088, up: 3.778, upvl: 3.95  }, ufc: { none: 0.45, up: 0.63, upvl: 0.68 } },
  { daily: 30, monthly: 900, cpc: { none: 3.588, up: 4.278, upvl: 4.45  }, ufc: { none: 0.45, up: 0.63, upvl: 0.68 } },
];

let ufcOn = false;

function setUFC(val) {
  ufcOn = val;
  document.getElementById('ufc-yes').classList.toggle('active', val);
  document.getElementById('ufc-no').classList.toggle('active', !val);
  updateURL();
  calc();
}

function calc() {
  const daily = parseInt(document.getElementById('daily').value);
  const tier = document.getElementById('tier').value;
  const row = DATA.find(r => r.daily === daily);
  
  const monthlyCPC = row.monthly;
  const ufcValue = ufcOn ? 300 : 0;
  const totalPackage = monthlyCPC + ufcValue;
  
  document.getElementById('monthly-out').textContent = '$' + monthlyCPC.toLocaleString();
  document.getElementById('cpc-out').textContent = row.cpc[tier].toFixed(3);
  document.getElementById('package-out').textContent = '$' + totalPackage.toLocaleString();
  
  const ufcEl = document.getElementById('ufc-out');
  if (ufcOn) {
    ufcEl.textContent = row.ufc[tier].toFixed(2);
    ufcEl.className = 'breakdown-value green';
  } else {
    ufcEl.textContent = '—';
    ufcEl.className = 'breakdown-value muted';
  }
  
  const total = ufcOn
    ? parseFloat((row.cpc[tier] + row.ufc[tier]).toFixed(3))
    : row.cpc[tier];
  document.getElementById('total-out').textContent = total.toFixed(3);
  
  updateURL();
}

function updateURL() {
  const daily = document.getElementById('daily').value;
  const tier = document.getElementById('tier').value;
  const ufc = ufcOn ? '1' : '0';
  const params = new URLSearchParams({ d: daily, t: tier, u: ufc });
  history.replaceState(null, '', '?' + params.toString());
}

function loadFromURL() {
  const params = new URLSearchParams(window.location.search);
  if (params.has('d')) document.getElementById('daily').value = params.get('d');
  if (params.has('t')) document.getElementById('tier').value = params.get('t');
  if (params.has('u')) setUFC(params.get('u') === '1');
  calc();
}

function copyLink() {
  const url = window.location.href;
  navigator.clipboard.writeText(url).then(() => {
    const btn = document.getElementById('copy-btn');
    btn.textContent = '✓ Copied!';
    btn.classList.add('copied');
    setTimeout(() => {
      btn.textContent = '📋 Copy Link';
      btn.classList.remove('copied');
    }, 2000);
  });
}

function resetCalc() {
  document.getElementById('daily').value = '10';
  document.getElementById('tier').value = 'none';
  setUFC(false);
  calc();
}

// Initialize
loadFromURL();
</script>
</body>
</html>
