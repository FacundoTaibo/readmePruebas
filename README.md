# ConsultaCFEApi.

Este proyecto API REST fue creado con SpringBoot en Java 8.

## &nbsp; &nbsp; Documentación del API REST.

URL testing [http://192.168.4.113:9090/ConsultaCFEApi/comprobante](http://192.168.4.113:9090/ConsultaCFEApi/comprobante)

### &nbsp; &nbsp; &nbsp; &nbsp; :point_right: Obtener tipos de comprobantes.

#### &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Request :arrow_upper_right:

Verbo: **`GET`**
<br>
Url: **/tiposComprobantes**

#### &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Response :leftwards_arrow_with_hook:

Respuesta exitosa: Status: **200 OK.** :heavy_check_mark:

<pre>
    <code>
        {
            "exito": true,
            "error": null,
            "datos": [
                {
                "tipoComprobante": 111,
                "tipo": "e-Factura",
                "indice": 0
                },
            ]
        }
    </code>
</pre>
<hr />

Respuesta con error: :x: Status: **500 Internal Server Error.**

<pre>
    <code>
        {
            "exito": false,
            "error": {
                "titulo": "Error obteniendo tipos de comprobantes",
                "mensaje": "Ocurrio un problema al obtener los tipos de comprobantes ",
                "mensajeException": "...",
                "severidad": "error"
            },
            "datos": null
        }
    </code>
</pre>
<hr /><hr />

### &nbsp; &nbsp; &nbsp; &nbsp; :point_right: Obtener comprobante.

#### &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Request :arrow_upper_right:

Verbo: **`GET`**
<br>

Url: **/comprobante?nombreCasilla=efac0200&tipoComprobante=111&montoTotal=9272.00&serie=A&codigoSeguridad=2cqFgy&numero=1**

#### &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Response :leftwards_arrow_with_hook:

Respuesta exitosa. Status: **200 OK.** :heavy_check_mark:

<pre>
    <code>
    {
        "exito": true,
        "error": null,
        "datos": {
            "nombreCasilla": "efac0200",
            "tipoComprobante": 111,
            "serieComprobante": "A ",
            "numeroComprobante": 1,
            "importeTotal": "9272.00",
            "codSeguridadDespachante": "2cqFgy",
            "codSeguridadDgi": "2cqFgyCQAbk5a+pMEvrc1woFLnk=",
            "formaDePago": "CREDITO",
            "rutCliente": "214894780010",
            "nombreCliente": "GABELUZ S.A.",
            "domicilioCliente": "HOCQUART 2124 ESQ.CUFRE",
            "fechaCfe": "09/03/2020",
            "monedaCfe": "UYU",
            "fechaFirmaComprobante": "2020-03-09T12:53:35-03:00",
            "fechaVencimientoComprobante": "09/03/2020",
            "cfeDeCobranza": 0,
            "importeNoFacturable": "-0000000000000000.50",
            "ivaTasaMinima": "10.00",
            "importeGravadoTasaMinima": "0.00",
            "importeIvaTasaMinima": "0.00",
            "ivaTasaBasica": "22.00",
            "importeGravadoTasaBasica": "3825.00",
            "importeIvaTasaBasica": "841.50",
            "importeExentoIva": "4606.00",
            "importeTotalCfe": "9272.50",
            "importeFinalCfe": "9272.00",
            "importeEntregasACuenta": "9272.00",
            "numeroRecibo": 31634,
            "numeroCae": "90200341419",
            "serieCfe": "A",
            "numeroInicialCae": 1,
            "numeroFinalCae": 3000,
            "fechaVencimientoCae": "04/03/2022",
            "items": [
                {
                "nombreCasilla": "efac0200",
                "tipoComprobante": 111,
                "serieComprobante": "A ",
                "numeroComprobante": 1,
                "indiceSecuencial": 1,
                "codigo": 201,
                "descripcion": "A.N.P.",
                "precioUnitario": "2176.00",
                "cantidadUnidades": "1.000",
                "importeTotal": "2176.00",
                "tipoIva": 1
                },
            ],
            "adendas": [
            {
                "nombreCasilla": "efac0200",
                "tipoComprobante": 111,
                "serieComprobante": "A ",
                "numeroComprobante": 1,
                "indiceSecuencial": 1,
                "textosVarios": "PERMISO D.N.A.: 36.194"
                },
                ],
                "tipo": {
                    "tipoComprobante": 111,
                    "tipo": "e-Factura",
                    "indice": 0
                },
                "urlCodigoQR": "",
                "textoSegunRut": "RUT Comprador",
                "datoSegunRut": "214894780010",
                "textoIvaTasaMinima": "10",
                "textoIvaTasaBasica": "22",
                "codSeguridadDgiEncode": "2cqFgyCQAbk5a%2BpMEvrc1woFLnk%3D",
                "numeroFacturaCompleto": "A-1"
        }
    }
    </code>
</pre>
<hr />

Respuesta con error

1. :x: En caso de enviar campos con información no válida se enviará la siguiente
   estructura indicando el error en cada campo con el **Status 400 BadRequest**:

<pre>
    <code>
        {
            "exito": false,
            "error": {
                "titulo": "Error intentando consultar un comprobante",
                "mensaje": "Alguno de los campos no tiene un valor válido",
                "mensajeException": "",
                "severidad": "error"
            },
            "datos": {
                "codigoSeguridad": "no puede estar vacío",
                "numero": "tiene que ser mayor o igual que 1",
                "serie": "No es una serie válida",
                "tipoComprobante": "tiene que ser mayor o igual que 1",
                "nombreCasilla": "La casilla es obligatoria",
                "montoTotal": "No es un monto válido, los decimales debe indicarse con
                \".\""
            }
        }
    </code>
</pre>
<hr />

2. :x: En caso de no encontrar el comprobante se enviará el siguiente mensaje con
   el **Status 400 BadRequest**:

<pre>
    <code>
        {
            "exito": false,
            "error": {
                "titulo": "Error obteniendo comprobante",
                "mensaje": "Ocurrio un problema al obtener el comprobante",
                "mensajeException": "No se encontro ningun comprobante según los datos
                enviados.",
                "severidad": "error"
            },
            "datos": null
        }
    </code>
</pre>
<hr />

3. :x: En caso de tener un error inesperado se devolverá la siguiente estructura con
   el **Status 500 Internal Server Error**:
   <pre>
       <code>
       {
           "exito": false,
           "error": {
               "titulo": "Error interno obteniendo comprobante",
               "mensaje": "Ocurrio una excepcion no esperada",
               "mensajeException": "...",
               "severidad": "error"
           },
           "datos": null
       }
       </code>
   </pre>
   <hr />
   <hr />

### &nbsp; &nbsp; &nbsp; &nbsp; :point_right: Obtener pdf comprobante.

#### &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Request :arrow_upper_right:

Verbo: **`GET`**
<br>

Url: **/comprobante?nombreCasilla=efac0200&tipoComprobante=111&montoTotal=9272.00&serie=A&codigoSeguridad=2cqFgy&numero=1**

#### &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Response :leftwards_arrow_with_hook:

Respuesta exitosa. Status: **200 OK.** :heavy_check_mark:

Headers:

- Content-Type: application/pdf.
- filename: serie-numeroFactura
- Body: matriz de bytes.

Respueta con errores.

**Se obtendrán las mismas respuestas con errores que en el endpoint “Obtener comprobante”.**

<hr />
<hr />

### &nbsp; &nbsp; &nbsp; &nbsp; :point_right: Registrar nuevo comprobante.

#### &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Request :arrow_upper_right:

Verbo: **`POST`**
<br>

Url: **/comprobante/_nombreCasilla_**
<br>
Head:
<br>

**Debe enviar la fecha en el formato que se especifica a continuación en el campo "fecha" y la suma de: año+mes+dia+hora+minuto aplicando el algoritmo RSA con su clave pública en el campo "Authorization", el Bearer prefijo no es obligatorio**

<br>
<pre>
    <code>
        {
            "fecha":"2022-05-20T08:01",
            "Authorization": "Bearer L19RLg1aeD7fXbmhGmr/RZGkF2IpNx2b6aSiuNivgiTFwrhXzVEyAQUV4HF/wbrVHAgKy26vfIWqNsRaCF80Zlo4wsepm3Yo/xYR4tLOi3ziHOClyn60evi/uXTObTYXj547vulpdkF0XEP840Ul44NJ9FPWv6eOkbQKm2Nn1vo="
        }
    </code>
</pre>

Body: en el cuerpo del request se debe enviar en texto plano el comprobante.

#### &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Response :leftwards_arrow_with_hook:

Respuesta exitosa. Status: **200 OK.** :heavy_check_mark:

<pre>
    <code>
    {
        "exito": true,
        "error": null,
        "datos": "Se agrego el comprobante con éxito!"
    }
    </code>
</pre>

Respuesta con error:

1. :x: En caso de enviar un comprobante que ya existe el status será **400 BadRequest** con la siguiente respuesta:
   <pre>
       <code>
           {
               "exito": false,
               "error": {
                   "titulo": "Error de validación del comprobante",
                   "mensaje": "Ya existe otro comprobante igual!",
                   "mensajeException": "Ya existe otro comprobante igual!",
                   "severidad": "error"
               },
               "datos": null
           }
       </code>
   </pre>
   <hr />

2. :x: En caso de enviar un comprobante no válido o una casilla no existente, el status será **400 BadRequest** con la siguiente respuesta:

<pre>
    <code>        
        {
            "exito": false,
            "error": {
                "titulo": "Error obteniendo empresa o convirtiendo el comprobante",
                "mensaje": "La empresa efac0201 no existe",
                "mensajeException": "La empresa efac0201 no existe",
                "severidad": "error"
            },
            "datos": null
        }
    </code>
</pre>
<hr />
<pre>
    <code>
    {
        "exito": false,
        "error": {
            "titulo": "Error obteniendo empresa o convirtiendo el comprobante",
            "mensaje": "La cantidad de campos del cabezal del comprobante no son
            válidos! Deben ser 6",
            "mensajeException": "La cantidad de campos del cabezal del
            comprobante no son válidos! Deben ser 6",
            "severidad": "error"
        },
        "datos": null
    }
    </code>
</pre>
<hr />
<pre>
    <code>
    {
        "exito": false,
        "error": {
            "titulo": "Error obteniendo empresa o convirtiendo el comprobante",
            "mensaje": "El texto enviado para convertir a comprobante esta
            vacío!",
            "mensajeException": "El texto enviado para convertir a comprobante
            esta vacío!",
            "severidad": "error"
        },
        "datos": null
    }
    </code>
</pre>
<hr />

3. :x: En caso de ocurrir un error inesperado el status será **500 Internal Server Error.**
4. :x: En caso de omitir la autorización o ser incorrecta el estado será **401 Unauthorized** con la siguiente respuesta:
   <pre>
       <code>
         {
              "exito": false,
              "error": {
                 "titulo": "Acceso denegado",
                 "mensaje": "Acceso denegado - Header incompleto para procesar la autenticación",
                 "mensajeException": "Acceso denegado - Header incompleto para procesar la autenticación",
                 "severidad": "error"
             },
             "datos": null
         }
       </code>
   </pre>
   <hr />
   O
   <pre>
       <code>
          {
              "exito": false,
              "error": {
                  "titulo": "Acceso denegado",
                  "mensaje": "Fecha con formato no válido. Formato válido: yyyy-MM-ddTHH:mm",
                  "mensajeException": "Fecha con formato no válido. Formato válido: yyyy-MM-ddTHH:mm",
                  "severidad": "error"
              },
              "datos": null
          }
       </code>
   </pre>
   <hr />
   O
   <pre>
       <code>
           {
               "exito": false,
               "error": {
                   "titulo": "Acceso denegado",
                   "mensaje": "Acceso denegado",
                   "mensajeException": "Acceso denegado",
                   "severidad": "error"
               },
               "datos": null
           }
       </code>
   </pre>

### &nbsp; &nbsp; &nbsp; &nbsp; :point_right: Obtener nombre de casilla dado dominio despachante.

#### &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Request :arrow_upper_right:

Verbo: **`GET`**
<br>

Url: **/empresa/obtenerCasilla/porDominio?dominio=http://cliente.mega6.com.uy/**

<ol>
    <li>http://cliente.mega6.com.uy/</li>
    <li>http://cliente.mega6.com.uy</li>
    <li>https://cliente.mega6.com.uy/</li>
    <li>https://cliente.mega6.com.uy</li>
    <li>http://www.cliente.mega6.com.uy/</li>
    <li>http://www.cliente.mega6.com.uy</li>
    <li>https://www.cliente.mega6.com.uy/</li>
    <li>https://www.cliente.mega6.com.uy</li>
    <li>cliente.mega6.com.uy/</li>
    <li>cliente.mega6.com.uy</li>
    <li>cliente</li>
</ol>

#### &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Response :leftwards_arrow_with_hook:

Respuesta exitosa. Status: **200 OK.** :heavy_check_mark:

<pre>
    <code>
        {
            "exito": true,
            "error": null,
            "datos": "efac0307"
        }
    </code>
</pre>

Respuesta con error:

1. :x: En caso de enviar en blanco o ser un dominio no válido el status sera 400
   BadRequest:

<pre>
    <code>
        {
            "exito": false,
            "error": {
                "titulo": "Sin resultados",
                "mensaje": "El dominio enviado esta en blanco o no es válido",
                "mensajeException": "El dominio enviado esta en blanco o no es válido",
                "severidad": "error"
            },
            "datos": null
        }
    </code>
</pre>
<hr />

2. :x: En caso de no existir el nombre de casilla dado un dominio el status sera 400
   BadRequest:

<pre>
    <code>
        {
            "exito": false,
            "error": {
                "titulo": "Sin resultados",
                "mensaje": "No existe una casilla para el dominio: http://clientePruebaInexistente",
                "mensajeException": "No existe una casilla para el dominio: http://clientePruebaInexistente",
                "severidad": "error"
            },
            "datos": null
        }
    </code>
</pre>
<hr />

3. :x: En caso de ocurrir un error inesperado el status será 500 Internal Server Error.
