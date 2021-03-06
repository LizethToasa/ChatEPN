# ChatEPN
**Asignatura:** Tópicos Especiales\
**Facultad:** ESFOT\
**Integrantes:**
* Lizeth Toasa
* Alberto Heredia
* Jhonathan Pizarra

**Descripción:**
Desarrollo de una aplicación de chat, donde se interactua con uno o varios usuarios registrados mediante mensajes de texto y fotos.
Que permitir que los usuarios inicien sesión en la aplicacion y de esa manera puedan sincronizar datos con Firebase Realtime Database.
Almacenando archivos en Firebase.

## API
Se desarrollo y se aplico en android sdk 6.0 api 23 marshmallow

## Funcionalidad
En lo que se trabajo en relación con la aplicación de chat es garantizar una funcionalidad ininterrumpida 
en los emuladores que se esta trabajando haciendo que tengan una experiencia casi idéntica a otras aplicaciones de chat cuando usen la 
aplicación, sin importar qué dispositivo o emulador se estén usando. 

Mostrando a continuacion una lista de las funciones disponibles de aplicaciones:
Se reciben los nuevos mensajes cuando la aplicación esté en segundo plano.
Los chats se mantendrán actualizados incluso cuando alternes entre nuestro panel en línea y la aplicación.
Inicia chats desde la aplicación cuando se tenga que preguntar en el chat.
Es necesario registrarse o legearse para poder interactuar en el chat.
Se interactua con los usuarios registrado de la aplicacion.
Se puede enviar mensajes de texto y fotos.

## Desarrollo
Se desarrollo en el entorno de desarrollo integrado (IDE) oficial para el desarrollo de apps para Android, utilizando tres dispositivos
para probar la aplicacion de chat los cuales son el emulador de bluestack, teléfono celular, y una tablet.

## Características
Mensajes instantáneos: Permite una interacción fluida mediante texto.
Imágenes: Permite compartir imágenes.
Discusión: Se puede utilizar en lugar del teléfono para hablar.
Capacidad móvil: Se permite enviar mensajes instantáneos desde emuladores, dispositivos moviles como el teléfono celular.
Registro: Al tener que registrarse para poder utilizar la aplicacion.
APK funcional.
Todas los mensajes quedan registrados para verlos posteriormente, y pueden ponerse a disposición del usuario.
Abierto las 24 horas del día todos los días. Internet y la totalidad de sus aplicaciones están disponibles las 24 horas del día todos 
los días. 

## Código
**Se comenzó por crear la base de datos y crear reglas para que los usuarios puedan escribir y leer**
android.enableJetifier=true
android.useAndroidX=true

![reglas](https://user-images.githubusercontent.com/38388351/88716263-6ee76200-d0e4-11ea-81e4-f185dc8a07f8.png)
![mail](https://user-images.githubusercontent.com/38388351/88716318-86bee600-d0e4-11ea-88f9-46e3e77a56d5.PNG)

@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        mSharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
        // Set default username is anonymous.
        mUsername = ANONYMOUS;

        //Autentica si está este usuario en mi Firebase
        mFirebaseAuth = FirebaseAuth.getInstance();
        mFirebaseUser = mFirebaseAuth.getCurrentUser();
        if (mFirebaseUser == null) {
            // Not signed in, launch the Sign In activity
            startActivity(new Intent(this, SignInActivity.class));
            finish();
            return;
        } else {
            mUsername = mFirebaseUser.getDisplayName();
            if (mFirebaseUser.getPhotoUrl() != null) {
                mPhotoUrl = mFirebaseUser.getPhotoUrl().toString();
            }
        }

        GoogleSignInOptions gso = new GoogleSignInOptions.Builder(GoogleSignInOptions.DEFAULT_SIGN_IN)
                .requestIdToken(getString(R.string.default_web_client_id))
                .requestEmail()
                .build();
        mSignInClient = GoogleSignIn.getClient(this, gso);



**Instanciamos las variables de la base de datos y de nuestro frame**

   public static class MessageViewHolder extends RecyclerView.ViewHolder {
        TextView messageTextView;
        ImageView messageImageView;
        TextView messengerTextView;
        CircleImageView messengerImageView;

        public MessageViewHolder(View v) {
            super(v);
            messageTextView = (TextView) itemView.findViewById(R.id.messageTextView);
            messageImageView = (ImageView) itemView.findViewById(R.id.messageImageView);
            messengerTextView = (TextView) itemView.findViewById(R.id.messengerTextView);
            messengerImageView = (CircleImageView) itemView.findViewById(R.id.messengerImageView);
        }

    }

    // Firebase variables
    private FirebaseAuth mFirebaseAuth;
    private FirebaseUser mFirebaseUser;
    private DatabaseReference mFirebaseDatabaseReference;
    private FirebaseRecyclerAdapter<ChatMessenger, MessageViewHolder>
            mFirebaseAdapter;

    private static final String TAG = "MainActivity";
    public static final String MESSAGES_CHILD = "messages";
    private static final int REQUEST_INVITE = 1;
    private static final int REQUEST_IMAGE = 2;
    private static final String LOADING_IMAGE_URL = "https://www.google.com/images/spin-32.gif";
    public static final int DEFAULT_MSG_LENGTH_LIMIT = 10;
    public static final String ANONYMOUS = "anonymous";
    private static final String MESSAGE_SENT_EVENT = "message_sent";

            
**Un activityClass.java, para el registro**

![SingIn](https://user-images.githubusercontent.com/38388351/88716752-254b4700-d0e5-11ea-80d0-e0f5430cc9ea.PNG)

## Un activityClass.java para el chat

package com.google.firebase.codelab.friendlychat;
public class ChatMessenger {

    private String id;
    private String text;
    private String name;
    private String photoUrl;
    private String imageUrl;

    public ChatMessenger(){}

    public ChatMessenger(String text, String name, String photoUrl, String imageUrl) {
        this.text = text;
        this.name = name;
        this.photoUrl = photoUrl;
        this.imageUrl = imageUrl;
    }

    public String getId() {return id;}
    public void setId(String id) {this.id = id;}
    public void setText(String text) {this.text = text;}
    public String getName() {return name;}
    public void setName(String name) {this.name = name;}
    public String getPhotoUrl() {return photoUrl;}
    public String getText() {return text;}
    public void setPhotoUrl(String photoUrl) {this.photoUrl = photoUrl;}
    public String getImageUrl() {return imageUrl;}
    public void setImageUrl(String imageUrl) {this.imageUrl = imageUrl;}

}


## Manual de uso
### Introducción
El chat se configura como una herramienta importante para que el usuario pueda contactarse. Se sobrelapa al mainActivity y permite que otros usuarios en tiempo real 
intermcabien mensajes, e imágenes. El horario de atención del chat se establece de forma ininterrumpida todos los dias y horas.
Cabe señalar que para la autenticación deberán registrarse por medio de Google.

### Acceso al chat
1. Para acceder al chat hay que hacer click en el enlace de la APK Generada.

![2](https://user-images.githubusercontent.com/38388351/88714036-d223c500-d0e1-11ea-9bc3-65046d3f0427.PNG)

2. Una vez en el enlace  tenemos que identificarnos como usuario, poniendo nuestro nombre y contraseña.

![Login](https://user-images.githubusercontent.com/38388351/88714169-0303fa00-d0e2-11ea-9fc8-abd8f65e0493.PNG)

![image](https://user-images.githubusercontent.com/23488888/88670682-fa440180-d0aa-11ea-9ff3-e6951f7faf94.png)

Los campos del formulario son los siguientes, empezando desde arriba:
Email Address o Dirección de Correo Electrónico: Pondremos una dirección de correo válida.
Password  o Contraseña: Introducimos una contraseña (si es segura mejor) para poder acceder a la aplicación.

Para terminar con el registro pulsamos el botón azul “Register”

![Login2](https://user-images.githubusercontent.com/38388351/88717353-09947080-d0e6-11ea-833c-05b0f7ce15bf.PNG)

3. Cuando ya nos hemos registrado iniciara el chat y nos aparecerá la ventana de conversación, donde podremos contestar el chat en 
cuestión. En el margen derecho a al final de la ventana veremos un boton de enviar.

![image](https://user-images.githubusercontent.com/23488888/88671313-c5847a00-d0ab-11ea-94a3-99c6ad9f22b5.png)

Por detrás luce así:

![metodosSesion](https://user-images.githubusercontent.com/38388351/88717556-511afc80-d0e6-11ea-996b-c53089f20a0e.PNG)

4. Y tambien podemos visualizar los chat creados ultimamente o dode se quedo la conversacion y se puede continuar

![chat1](https://user-images.githubusercontent.com/38388351/88714275-2f1f7b00-d0e2-11ea-9b0c-e9e859e24c35.PNG)

5. Aplicamos estilos, cambiando de icono y colores en nuestra aplicación:
![Icono](https://user-images.githubusercontent.com/38388351/88713356-caafec00-d0e0-11ea-9528-724791d764a0.PNG)
![Paletta](https://user-images.githubusercontent.com/38388351/88713501-03e85c00-d0e1-11ea-8ad3-13dfa48b8c03.PNG)
![SlpashScreen](https://user-images.githubusercontent.com/38388351/88713788-6fcac480-d0e1-11ea-98bf-712d83e484e1.png)



**Refrencias:**\

*Manual de creación de chat:* https://codelabs.developers.google.com/codelabs/firebase-android/#0 

*código base:* https://github.com/firebase/codelab-friendlychat-android

*Tutorial en Youtube:* https://www.youtube.com/watch?v=xxXcxyDDIcU&feature=youtu.be

  




