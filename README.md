# labo7_web

¿Cuál es la diferencia entre autenticación y autorización?
Esta es una de las distinciones más importantes en seguridad:

Autenticación (Quién eres): Es el proceso de verificar tu identidad. Se trata de probar que eres quien dices ser.

Ejemplo: Cuando inicias sesión con tu usuario y contraseña. Estás autenticándote.

Analogía: Mostrar tu documento de identidad (DNI o pasaporte) para entrar a un edificio.

Autorización (Qué puedes hacer): Es el proceso de verificar tus permisos. Una vez que el sistema sabe quién eres (autenticación), determina qué tienes permitido hacer.

Ejemplo: Un usuario "normal" puede ver su propio perfil, pero un usuario "administrador" puede editar o borrar los perfiles de otros usuarios.

Analogía: Una vez dentro del edificio (autenticado), tu tarjeta de acceso (autorización) solo te permite entrar a tu oficina (piso 5), pero no al cuarto de servidores (piso 10).

¿Cuál es la función del token JWT en la guía?
En la arquitectura de esa guía (React en el frontend, Express en el backend), el frontend y el backend son aplicaciones separadas que no comparten estado. Necesitan una forma de que el backend "recuerde" al usuario en cada petición.

La función del Token JWT (JSON Web Token) es actuar como una credencial digital segura que prueba que el usuario ya se ha autenticado.

El flujo es el siguiente:

Login: El usuario envía su email y contraseña desde React a Express.

Creación del Token: El servidor Express verifica los datos. Si son correctos, crea un token JWT. Este token es una cadena de texto larga que contiene información del usuario (como su ID) y está "firmada" digitalmente por el servidor.

Envío al Cliente: El servidor envía este token de vuelta a React.

Almacenamiento: React guarda este token en el Local Storage del navegador (como indica la guía).

Prueba de Identidad: Ahora, para cada futura petición que React haga al backend (como pedir datos del perfil), adjuntará automáticamente ese token (normalmente en la cabecera Authorization).

Verificación: El middleware VerifyToken en Express intercepta esa petición, mira el token, comprueba la firma digital y, si es válida, sabe quién es el usuario y le da acceso al recurso.
