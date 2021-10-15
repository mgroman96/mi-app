# Mi app

## Creacion:
    npx create-react-app mi-app
## Inicializarla:
    npm start

## Componentes

### context:

**cartContext funciones**

*addItem: agregar productos al carrito y verificar que no esten repetidos

*isInCar: buscar el producto dentro del carrito returna true o false

removeItem: recibe por props un id y setea al carrito un array filtrado 

clear: vacia el carrito

getTotal: recorre el carrito y calculay returna el total

getQuantity: recorre el carrito y cuenta y returna las cantidades

**userContext funciones:**

login: recibe el nombre de osuario y lo guarda en un estado

logout: vacia el estado

### firebase:

Utilizo firebase.js para traer documentacion de la base de datos y exportarla a los componentes de mi-app 

funciones que exporta:

categorias(): returna una promesa con todas las categorias de la base de datos

getArticles(): recibe tres props, si las tres son verdaderas retorna una promesa con los productos filtrados, si no lo son retorna todos los productos.

articleById(): recibe por props un id y busca en la base de datos y retorna un solo articulo.

sendOrder(): recibe un objeto por props, revisa si hay stock disponible para todos los objetos pedidos, si no hay los pushea a un array, luego si el array esta vacio agrega los pedidos a la base de datos. y retorna una promesa de succes o error

### navBar:
Utileze la funcion categorias() la cual retorna una promise con las categorias importada de "firebase.js", luego las guarde en un estado "category" y las mapie dentro del navBar.

Importo las funciones logout y user del context userContext y linkeo el login para iniciar sesion.
Tambien importo getQuantity y clear del context carContext para agregar la cantidad al carrito y para vaciar el carrito cuando se cierra sesion.

### cart:

recibe las funciones "clear", "getTotal" y los "articulos" del [cartContext]() y el "user" del [userContext](), mapea los articulos por props en el itemCart donde los muestra.
Retorna los articulos y los botones vaciar carrito, confirmar compra(pasa por props el carrito y recibe una promesa) y el total

### itemCount:

recibe "addItem", "isInCar","getProduct" del cartContext. luego dentro de un useEffect utilizo isIncar y si es verdadero tambien getProduct para setear la cantidad a un estado.Luego retorno la cantidad del estado y los botones para agregar (sin pasarme del stock que recibi por props),restar , y el boton agregar al carrito que ejecuta la funcion addItem

### itemDetailContainer:

recibo un id por usePArams
utilizo articlebyId con el id dentro del useEffect y que actualize cada que cambia el id, agrego el articulo a un estado y lo mando por props al componente itemDetail

itemDetail: retorna la ficha de detalles del producto. Recibe el usuario del contexto userContext, si esta logeado muesta el componente itemCount tambien el boton de ir al carrito, sino muestra un boton para logearse

### itemCount:

importa addItem, isInCar, getProduct del contexto carContext y un estado para almacenar la cantidad. Dentro del useEffect verifico con isInCar si el objeto esta en el carrito y si esta traigo la cantidad con getProduct y seteo la cantidad al estado.

retorno la cantidad con los botones para agregar,quitar unidades y agregar al carrito con la funcion addItem

### login:

importa la funcion login del context userContext, useHistory de react-router-dom y crea los estados username y password. retorna un formulario donde utiliza el evento onChange en el input para setear los estados y un boton de submit. cuando se envia el formulario se activa la funcion handleLogin que envia el objeto con los estados a la funcion login del userContext y pushea el history al home.