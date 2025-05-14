# Notas sobre Directivas de Preprocesador en Unity

## Sintaxis Básica
```csharp
#if CONDICIÓN
    // código que se compila si la condición es verdadera
#elif OTRA_CONDICIÓN
    // código que se compila si la primera condición es falsa y esta es verdadera
#else
    // código que se compila si todas las condiciones anteriores son falsas
#endif
```

## Formas de Definir Directivas
1. **Editor de Unity**
   - Edit > Project Settings > Player > Other Settings > Scripting Define Symbols
   - Añadir el símbolo (ej: ENABLE_INPUT_SYSTEM)

2. **En el código**
   ```csharp
   #define ENABLE_INPUT_SYSTEM
   ```

3. **Archivo de proyecto (.csproj)**
   ```xml
   <PropertyGroup>
     <DefineConstants>ENABLE_INPUT_SYSTEM</DefineConstants>
   </PropertyGroup>
   ```

4. **Package Manager**
   - Algunas directivas se definen automáticamente al instalar paquetes

## Directivas Vinculadas a Paquetes
1. **ENABLE_INPUT_SYSTEM**
   - Paquete: com.unity.inputsystem
   - Se activa con el nuevo sistema de entrada

2. **ENABLE_LEGACY_INPUT_MANAGER**
   - Sistema de entrada heredado
   - Activo por defecto

3. **ENABLE_VR**
   - Paquete: com.unity.xr
   - Se activa con el paquete de realidad virtual

4. **ENABLE_URP**
   - Paquete: com.unity.render-pipelines.universal
   - Se activa con Universal Render Pipeline

5. **ENABLE_HDRP**
   - Paquete: com.unity.render-pipelines.high-definition
   - Se activa con High Definition Render Pipeline

## Directivas de Plataforma
- UNITY_EDITOR
- UNITY_ANDROID
- UNITY_IOS
- UNITY_STANDALONE_WIN

## Características Importantes
- Se evalúan en tiempo de compilación, no en tiempo de ejecución
- Permiten adaptar el código según los paquetes instalados
- Útiles para mantener compatibilidad con diferentes versiones de Unity
- Ayudan a manejar diferentes sistemas (como el caso del Input System)

## Estructura Try-Catch
```csharp
try
{
    // Código que podría generar una excepción
    // Por ejemplo: acceder a un objeto que podría ser null
}
catch (TipoDeExcepcion ex)
{
    // Código para manejar la excepción
    // Por ejemplo: registrar el error o mostrar un mensaje
}
```

### Uso Común
1. **Manejo de NullReferenceException**
   ```csharp
   try
   {
       objeto.Método();
   }
   catch (NullReferenceException)
   {
       Debug.Log("El objeto es null");
   }
   ```

2. **Manejo de Excepciones Específicas**
   ```csharp
   try
   {
       // Código que podría fallar
   }
   catch (FileNotFoundException ex)
   {
       // Manejar error de archivo no encontrado
   }
   catch (UnauthorizedAccessException ex)
   {
       // Manejar error de acceso no autorizado
   }
   catch (Exception ex)
   {
       // Manejar cualquier otra excepción
   }
   ```

3. **Finally (Opcional)**
   ```csharp
   try
   {
       // Código que podría fallar
   }
   catch (Exception ex)
   {
       // Manejar la excepción
   }
   finally
   {
       // Código que siempre se ejecuta
       // Útil para liberar recursos
   }
   ```

### Casos de Uso Comunes
- Acceso a objetos que podrían ser null
- Operaciones de archivo
- Conexiones a bases de datos
- Llamadas a APIs externas
- Operaciones de red
- Acceso a recursos del sistema

### Buenas Prácticas
- Usar try-catch solo cuando es necesario
- Capturar excepciones específicas en lugar de Exception genérica
- Incluir mensajes de error descriptivos
- Liberar recursos en bloques finally
- No usar try-catch para control de flujo normal
- Registrar excepciones para debugging 