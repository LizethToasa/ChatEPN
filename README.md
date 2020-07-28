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
### Se utilizaron las siguientes librerias para el funcionamiento del la aplicación de chat

import android.content.Intent;
import android.content.SharedPreferences;
import android.net.Uri;
import android.os.Bundle;
import android.preference.PreferenceManager;
import android.text.Editable;
import android.text.TextWatcher;
import android.util.Log;
import android.view.LayoutInflater;
import android.view.Menu;
import android.view.MenuInflater;
import android.view.MenuItem;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ImageView;
import android.widget.ProgressBar;
import android.widget.TextView;
import android.widget.Toast;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.content.ContextCompat;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;

import com.bumptech.glide.Glide;
import com.firebase.ui.database.FirebaseRecyclerAdapter;
import com.firebase.ui.database.FirebaseRecyclerOptions;
import com.firebase.ui.database.SnapshotParser;
import com.google.android.gms.auth.api.signin.GoogleSignIn;
import com.google.android.gms.auth.api.signin.GoogleSignInClient;
import com.google.android.gms.auth.api.signin.GoogleSignInOptions;
import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.firebase.auth.FirebaseAuth;
import com.google.firebase.auth.FirebaseUser;
import com.google.firebase.database.DataSnapshot;
import com.google.firebase.database.DatabaseError;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;
import com.google.firebase.storage.FirebaseStorage;
import com.google.firebase.storage.StorageReference;
import com.google.firebase.storage.UploadTask;

import de.hdodenhof.circleimageview.CircleImageView;

### Instanciamos las variables de la base de datos

    private FirebaseAuth mFirebaseAuth;
    private FirebaseUser mFirebaseUser;
    private DatabaseReference mFirebaseDatabaseReference;
    private FirebaseRecyclerAdapter<FriendlyMessage, MessageViewHolder>
            mFirebaseAdapter;
            
### Un java.class y se agrega los campos que se pediran en el registro

public class FriendlyMessage {

    private String id;
    private String text;
    private String name;
    private String photoUrl;
    private String imageUrl;

    public FriendlyMessage() {
    }

    public FriendlyMessage(String text, String name, String photoUrl, String imageUrl) {
        this.text = text;
        this.name = name;
        this.photoUrl = photoUrl;
        this.imageUrl = imageUrl;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public void setText(String text) {
        this.text = text;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPhotoUrl() {
        return photoUrl;
    }

    public String getText() {
        return text;
    }

    public void setPhotoUrl(String photoUrl) {
        this.photoUrl = photoUrl;
    }

    public String getImageUrl() {
        return imageUrl;
    }

    public void setImageUrl(String imageUrl) {
        this.imageUrl = imageUrl;
    }
}

## Manual de uso
### Introducción
El chat se configura como una herramienta importante para que el usuario pueda contactarse. El horario de atención del chat se establece 
de forma ininterrumpida todos los dias y horas.

### Acceso al chat
1. Para acceder al chat hay que hacer click en el enlace de la APK Generada.

![image](https://user-images.githubusercontent.com/23488888/88690871-bdcfd000-d0c1-11ea-8931-5338b0dd224e.png)

2. Una vez en el enlace  tenemos que identificarnos como usuario, poniendo nuestro nombre y contraseña.

![image](https://user-images.githubusercontent.com/23488888/88670360-94f01080-d0aa-11ea-93ca-f4e064d31cce.png)

![image](https://user-images.githubusercontent.com/23488888/88670682-fa440180-d0aa-11ea-9ff3-e6951f7faf94.png)

Los campos del formulario son los siguientes, empezando desde arriba:
Email Address o Dirección de Correo Electrónico: Pondremos una dirección de correo válida.
Password  o Contraseña: Introducimos una contraseña (si es segura mejor) para poder acceder a la aplicación.

Para terminar con el registro pulsamos el botón azul “Register”

3. Cuando ya nos hemos registrado iniciara el chat y nos aparecerá la ventana de conversación, donde podremos contestar el chat en 
cuestión. En el margen derecho a al final de la ventana veremos un boton de enviar.

![image](https://user-images.githubusercontent.com/23488888/88671313-c5847a00-d0ab-11ea-94a3-99c6ad9f22b5.png)


4. Y tambien podemos visualizar los chat creados ultimamente o dode se quedo la conversacion y se puede continuar

![image](https://user-images.githubusercontent.com/23488888/88671556-0d0b0600-d0ac-11ea-848e-6507804b373a.png)







  




