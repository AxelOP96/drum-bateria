# drum-bateria
 simulador de bateria utilizando las teclas como notas musicales
*Para comenzar, en el documento HTML, dentro de un div contenedor colocamos varios divs a los cuales se les asigna un data-key y una clase general, ademas de la etiqueta kbd que sirve para que el usuario sepa que tecla apretar y que con el nombre de la nota sepa que sonido tiene asignado. EL data-key que se le asignó se obtuvo de la pagina http://keycode.info/ que a cada tecla le asigna un valor. 
 Si queres hacer algo como una key en el HTML, es conveniente usar data-key ya que linkea elementos por ejemplo en este repositorio las teclas y los sonidos correspondientes.
 
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
 
 
 Esta funcion hace que al ejecutarse el evento, si no tiene que transformarse  entonces remueve la clase playing. para que al apretar una tecla no quite las clases de las demas.
 
 function removeTransition(e) {
  if (e.propertyName !== 'transform') return;
  e.target.classList.remove('playing');
}

*Se crea una funcion en la que la constante audio toma el selector de clase key donde al activarse el elemento audio accede al keycode correspondiente de esa tecla. La constante key 

function playSound(e) {
  const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
  
  *Para agregar la animacion utilizo la constante anterior y en vez de utilizar el elemento audio utilizo el los divs con clase key
  
  const key = document.querySelector(`div[data-key="${e.keyCode}"]`);
  
  *Para que solo las teclas seleccionadas generen sonido y no devuelva un valor indefinido usamos un condicional que detendra la funcion de correr completamente.
  
  if (!audio) return;
  
 * Esto agrega a la clase key una clase adicional que es playing para ejecutar la animacion correspondiente luego de darle clic a cada letra.
  
  key.classList.add('playing');
  
  *Para reiniciar el audio una y otra vez y no tener que esperar a que termine de sonar para ejecutar otro sonido se usa 
  
  audio.currentTime = 0;
  
 * Para escuchar el audio
  
  audio.play();
}

*Para escuchar cuando cada tecla se oprima y podamos fijar un fin de la transicion se creaa una constante que selecciona todas los elementos con clase key

const keys = Array.from(document.querySelectorAll('.key'));

*Ahora se quiere escuchar es el evento llamado transition end en cada uno.Tomamos el elemento con clase keys y usamos un for each (sirve para moverse por los elementos de una estructra de datos, como podría ser un vector, y realizar acciones para cada una de los elementos) para movernos por los key. Usamos un arrow function(son funciones anónimas con una sintaxis más compacta y que aparte de la diferencia en la sintaxis también tienen algunas peculiaridades como que no vinculan su propio this o que no se pueden usar como constructores) para que cada key al usar el addEventListener escuche el TransitionEnd y active el removeTransition para darle fin.

keys.forEach(key => key.addEventListener('transitionend', removeTransition));

al escuchar el evento keydown ejecuta la funcion playSound

window.addEventListener('keydown', playSound);
 
 
 aplicación:
 https://drum-bateria.vercel.app/
