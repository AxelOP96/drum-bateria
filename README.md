# drum-bateria
 simulador de bateria utilizando las teclas como notas musicales
 Para comenzar en el documento HTML, dentro de un div contenedor colocamos varios divs a los cuales se les asigna un data-key y una clase general, ademas de la etiqueta kbd que sirve para que el usuario sepa que tecla apretar y que sepa que sonido tiene asignado.
 
 
 <div class="keys">
        <div data-key="65" class="key"><kbd>A</kbd><span class="sound">clap</span></div>
        <div data-key="83" class="key"><kbd>S</kbd><span class="sound">hihat</span></div>
        <div data-key="68" class="key"><kbd>D</kbd><span class="sound">kick</span></div>
        <div data-key="70" class="key"><kbd>F</kbd><span class="sound">openhat</span></div>
        <div data-key="71" class="key"><kbd>G</kbd><span class="sound">boom</span></div>
        <div data-key="72" class="key"><kbd>H</kbd><span class="sound">ride</span></div>
        <div data-key="74" class="key"><kbd>J</kbd><span class="sound">snare</span></div>
        <div data-key="75" class="key"><kbd>K</kbd><span class="sound">tom</span></div>
        <div data-key="76" class="key"><kbd>L</kbd><span class="sound">tink</span></div>
        </div>
 
 
 function removeTransition(e) {
  if (e.propertyName !== 'transform') return;
  e.target.classList.remove('playing');
}

function playSound(e) {
  const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
  const key = document.querySelector(`div[data-key="${e.keyCode}"]`);
  if (!audio) return;
  key.classList.add('playing');
  audio.currentTime = 0;
  audio.play();
}

const keys = Array.from(document.querySelectorAll('.key'));
keys.forEach(key => key.addEventListener('transitionend', removeTransition));
window.addEventListener('keydown', playSound);
 
 
 aplicación:
 https://drum-bateria.vercel.app/
