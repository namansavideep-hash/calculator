# calculator    it is made with some help of  Ai

<h2 class="sr-only">Addition-only calculator</h2>
<div style="max-width: 320px; margin: 2rem auto; background: var(--color-background-primary); border: 0.5px solid var(--color-border-tertiary); border-radius: var(--border-radius-lg); padding: 1.5rem; font-family: var(--font-sans);">
  <div id="display" style="background: var(--color-background-secondary); border: 0.5px solid var(--color-border-tertiary); border-radius: var(--border-radius-md); padding: 1rem 1.25rem; text-align: right; margin-bottom: 1rem; min-height: 64px;">
    <div id="expr" style="font-size: 13px; color: var(--color-text-secondary); min-height: 18px; word-break: break-all;"></div>
    <div id="result" style="font-size: 28px; font-weight: 500; color: var(--color-text-primary);">0</div>
  </div>

  <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 8px;">
    <button onclick="clearAll()" style="grid-column: span 2; padding: 14px; font-size: 15px; border-radius: var(--border-radius-md); border: 0.5px solid var(--color-border-secondary); background: var(--color-background-secondary); color: var(--color-text-primary); cursor: pointer;">AC</button>
    <button onclick="backspace()" style="padding: 14px; font-size: 15px; border-radius: var(--border-radius-md); border: 0.5px solid var(--color-border-secondary); background: var(--color-background-secondary); color: var(--color-text-primary); cursor: pointer;">⌫</button>
    <button onclick="addOp()" style="padding: 14px; font-size: 18px; font-weight: 500; border-radius: var(--border-radius-md); border: 0.5px solid var(--color-border-secondary); background: var(--color-background-info); color: var(--color-text-info); cursor: pointer;">+</button>

    <button onclick="digit('7')" style="padding: 14px; font-size: 16px; border-radius: var(--border-radius-md); border: 0.5px solid var(--color-border-tertiary); background: var(--color-background-primary); color: var(--color-text-primary); cursor: pointer;">7</button>
    <button onclick="digit('8')" style="padding: 14px; font-size: 16px; border-radius: var(--border-radius-md); border: 0.5px solid var(--color-border-tertiary); background: var(--color-background-primary); color: var(--color-text-primary); cursor: pointer;">8</button>
    <button onclick="digit('9')" style="padding: 14px; font-size: 16px; border-radius: var(--border-radius-md); border: 0.5px solid var(--color-border-tertiary); background: var(--color-background-primary); color: var(--color-text-primary); cursor: pointer;">9</button>
    <div></div>

    <button onclick="digit('4')" style="padding: 14px; font-size: 16px; border-radius: var(--border-radius-md); border: 0.5px solid var(--color-border-tertiary); background: var(--color-background-primary); color: var(--color-text-primary); cursor: pointer;">4</button>
    <button onclick="digit('5')" style="padding: 14px; font-size: 16px; border-radius: var(--border-radius-md); border: 0.5px solid var(--color-border-tertiary); background: var(--color-background-primary); color: var(--color-text-primary); cursor: pointer;">5</button>
    <button onclick="digit('6')" style="padding: 14px; font-size: 16px; border-radius: var(--border-radius-md); border: 0.5px solid var(--color-border-tertiary); background: var(--color-background-primary); color: var(--color-text-primary); cursor: pointer;">6</button>
    <div></div>

    <button onclick="digit('1')" style="padding: 14px; font-size: 16px; border-radius: var(--border-radius-md); border: 0.5px solid var(--color-border-tertiary); background: var(--color-background-primary); color: var(--color-text-primary); cursor: pointer;">1</button>
    <button onclick="digit('2')" style="padding: 14px; font-size: 16px; border-radius: var(--border-radius-md); border: 0.5px solid var(--color-border-tertiary); background: var(--color-background-primary); color: var(--color-text-primary); cursor: pointer;">2</button>
    <button onclick="digit('3')" style="padding: 14px; font-size: 16px; border-radius: var(--border-radius-md); border: 0.5px solid var(--color-border-tertiary); background: var(--color-background-primary); color: var(--color-text-primary); cursor: pointer;">3</button>
    <div></div>

    <button onclick="digit('0')" style="grid-column: span 2; padding: 14px; font-size: 16px; border-radius: var(--border-radius-md); border: 0.5px solid var(--color-border-tertiary); background: var(--color-background-primary); color: var(--color-text-primary); cursor: pointer;">0</button>
    <button onclick="dot()" style="padding: 14px; font-size: 16px; border-radius: var(--border-radius-md); border: 0.5px solid var(--color-border-tertiary); background: var(--color-background-primary); color: var(--color-text-primary); cursor: pointer;">.</button>
    <button onclick="calculate()" style="padding: 14px; font-size: 18px; font-weight: 500; border-radius: var(--border-radius-md); border: none; background: var(--color-text-primary); color: var(--color-background-primary); cursor: pointer;">=</button>
  </div>
</div>

<script>
let current = '0';
let expression = [];
let justCalc = false;

function updateDisplay() {
  document.getElementById('result').textContent = current;
  document.getElementById('expr').textContent = expression.join(' ');
}

function digit(d) {
  if (justCalc) { current = d; expression = []; justCalc = false; }
  else current = current === '0' ? d : current + d;
  updateDisplay();
}

function dot() {
  if (justCalc) { current = '0.'; expression = []; justCalc = false; }
  else if (!current.includes('.')) current += '.';
  updateDisplay();
}

function addOp() {
  justCalc = false;
  expression.push(current, '+');
  current = '0';
  updateDisplay();
}

function calculate() {
  if (expression.length === 0) return;
  expression.push(current);
  let total = expression.filter((_, i) => i % 2 === 0).map(Number).reduce((a, b) => a + b, 0);
  let parts = expression.join(' ');
  expression = [];
  current = String(parseFloat(total.toFixed(10)));
  document.getElementById('expr').textContent = parts + ' =';
  document.getElementById('result').textContent = current;
  justCalc = true;
}

function clearAll() {
  current = '0'; expression = []; justCalc = false;
  updateDisplay();
}

function backspace() {
  if (justCalc) return;
  current = current.length > 1 ? current.slice(0, -1) : '0';
  updateDisplay();
}
</script>

