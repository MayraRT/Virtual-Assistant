# Virtual-Assistant
<!DOCTYPE html >
<html>

<head>
    <title>Asistente Virtual</title>
    <script  src ="//cdnjs.cloudflare.com/ajax/libs/annyang/2.6.0/annyang.min.js"></script>
    <script>
        if (annyang) {
            //Variable para almacenar las voces de nuestro sistema.
            var voices;
            //Inicializamos utter.
            var utter = new SpeechSynthesisUtterance();
            utter.rate = 1;
            utter.pitch = 0.5;
            utter.lang = 'en';

            //Cargamos las voces que tenemos en nuestro sistema y las mostarmos en un arreglo por consola.
            window.speechSynthesis.onvoiceschanged = function () {
                voices = window.speechSynthesis.getVoices();
                console.log(voices);
            };

            //Definimos los comandos a utilizar.
            var commands = {
                'hello AVA': function () {
                    utter.text = 'HELLO!';
                    //Setea la voz que queremos usar en base a nuestra lista.
                    utter.voice = voices[2];
                    window.speechSynthesis.speak(utter);
                },
                'HOW ARE YOU?': function () {
                    utter.text = 'IM FINE, THANKS!';
                    utter.voice = voices[2];
                    window.speechSynthesis.speak(utter);
                },
                'HELLO!': function () {
                    utter.text = 'HELLO, WHAT IS YOUR NAME?';
                    utter.voice = voices[2];
                    window.speechSynthesis.speak(utter);
                    //Guarda el nombre que le decimos por voz.
                    annyang.addCallback('result', function (phrases) {
                        //Imprime el nombre por consola.
                        console.log("Nombre: ", phrases[0]);
                        //Para el evento result.
                        annyang.removeCallback('result');
                        //Nos dice hola + el nombre que le digamos por voz.
                        utter.text = 'HELLO, ' + phrases[0];
                        window.speechSynthesis.speak(utter);
                    });
                },
                //Array que devuelve aleatoriamente un elemento del array, en este caso un chiste.
                'AVA, TELL ME A JOKE': function () {
                    chistes = ['Por qu?? las focas del circo miran siempre hacia arriba?   Porque es donde est??n los focos.',
                        'Estas obsesionado con la comida!   No se a que te refieres croquetamente.',
                        'Por que est??s hablando con esas zapatillas?   Porque pone "converse"',
                        'Buenos dias, me gustaria alquilar "Batman Forever".   No es posible, tiene que devolverla tomorrow.'
                    ];
                    utter.text = chistes[Math.floor(Math.random() * chistes.length)]
                    utter.voice = voices[2];
                    window.speechSynthesis.speak(utter);
                }
            };

            //Esto nos sirve para ver que escucha el programa en tiempo real.

            annyang.addCallback('result', function(phrases) {
            console.log("I think the user said: ", phrases[0]);
            console.log("But then again, it could be any of the following: ", phrases);
            });
   


            //Sumamos todos los comandos a annyang.
            annyang.addCommands(commands);

            //Annyang comienza a escuchar.
            annyang.start({ autoRestart: false, continuous: true });
            }
    </script>
</head>

<body>
    <h1 style="text-align: center;">A.V.A (Another Virtual Assistant)<br></h1>
    <div align="center"><img src="https://www.eluniversal.com.mx/sites/default/files/2021/04/13/jarvis-ya-es-real-nvidia-presenta-su-asistente-virtual.jpg" width="630" height="420"></div>
    <br>
    <br> 
    <FONT FACE="courier" SIZE=6>SAY HELLO TO AVA! </FONT>
    <br>
    <FONT FACE="courier" SIZE=5>
        YOU CAN USE THE NEXT COMMANDS:<br>
        'HELLO!' OR 'HELLO AVA!'<br>
    </FONT>
    <br>
    <br>
    <FONT FACE="courier" SIZE=6>ASK AVA TO TELL YOU A JOKE</FONT>
    <br>
    <FONT FACE="courier" SIZE=5>
        YOU CAN USE THE NEXT COMMAND:<br>
        'AVA, TELL ME A JOKE'<br>
    </FONT>
    <br>
    <button  class ="button" style="text-align: center;">MICROPHONE</button>
</body>

</html>
