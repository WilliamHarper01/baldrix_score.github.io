<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>Baldrix Score</title>
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <style>
    body { font-family: Segoe UI, Roboto, Arial, sans-serif; padding: 1rem; }
    label { display: block; margin: .5rem 0; }
    input[type="number"] { width: 8rem; margin-left: .5rem; }
    button { margin-top: .5rem; }
    .teams {
    display: flex;
    gap: 4rem;
    align-items: flex-start;
}
    .ilabel {
        min-width: 16em;
    }
    strong{
        font-size: 24px;
    }
  </style>
</head>
<body onload="start()">
  <div class="teams">

    <div class="team">
    <h1>Team Left</h1>

  <label class="ilabel" for="la">Magic:
    <input id="la" type="number" step="any" inputmode="decimal" value="0"/>
  </label>

  <label class="ilabel" for="lb">P3 Deaths:
    <input id="lb" type="number" step="any" inputmode="decimal" value="0"/>
  </label>

  <label class="ilabel" for="lc">Fast Clear:
    <input id="lc" type="checkbox" />
  </label>

  <strong> Score: </strong><strong id="lresult">0</strong>

  </div>

  <div class="team">
    <h1>Team Right</h1>

  <label class="ilabel" for="ra">Magic:
    <input id="ra" type="number" step="any" inputmode="decimal" value="0"/>
  </label>

  <label class="ilabel" for="rb">P3 Deaths:
    <input id="rb" type="number" step="any" inputmode="decimal" value="0"/>
  </label>

    <label class="ilabel" for="rc">Fast Clear:
    <input id="rc" type="checkbox" />
  </label>

  <strong> Score: </strong></strong><strong id="rresult">0</strong>

  </div>

  </div>

  <script>
    const la = document.getElementById('la');
    const lb = document.getElementById('lb');
    const lc = document.getElementById('lc');
    const lresult = document.getElementById('lresult');

    const ra = document.getElementById('ra');
    const rb = document.getElementById('rb');
    const rc = document.getElementById('rc');
    const rresult = document.getElementById('rresult');

    function lmultiply() {
      const va = parseFloat(la.value) || 0;
      const vb = parseFloat(lb.value) || 0;
      var vc = lc.checked;
      var prod = 1000 - (va) - (25*vb) + ((0+vc)*100);
      lresult.textContent = Number.isFinite(prod) ? prod : '0';
    }

    function rmultiply() {
      const va = parseFloat(ra.value) || 0;
      const vb = parseFloat(rb.value) || 0;
      var vc = rc.checked;
      var prod = 1000 - (va) - (25*vb) + ((0+vc)*100);
      rresult.textContent = Number.isFinite(prod) ? prod : '0';
    }

    function lwin() {
        rc.checked = !lc.checked;
        rmultiply();
        lmultiply();
    }

    function rwin() {
        lc.checked = !rc.checked;
        rmultiply();
        lmultiply();
    }

    function start(){
      rmultiply();
      lmultiply();
    }

    // live update when inputs change
    la.addEventListener('input', lmultiply);
    lb.addEventListener('input', lmultiply);
    lc.addEventListener('change', lwin);

    // live update when inputs change
    ra.addEventListener('input', rmultiply);
    rb.addEventListener('input', rmultiply);
    rc.addEventListener('change', rwin);
  </script>
</body>
</html>