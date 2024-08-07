# DocsConfig
```java

@Target({ElementType.TYPE, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Operation()
@ApiResponses(
/*Pending
  value = {
     @ApiResponse(
       responseCode = "200", description = "Success", content = {
       @Content(mediaType = "application/json", schema = @Schema(implementation = SomeClass.class))
     }
     ),
*/
    @ApiResponse(
      responseCode = "404", description = "Not Found", content = @Content
    ),
    @ApiResponse(
      responseCode = "422", description = "Invalid Data", content = @Content
    ),
    @ApiResponse(
      responseCode = "500", description = "System Error", content = @Content
    )
  }
)
public @interface DefaultDocs {
  @AliasFor(annotation = Operation.class, attribute = "summary")
  String value() default "";

/* ERROR:
@AliasFor declaration on attribute 'schemaClass' in annotation {...}
declares an alias for attribute 'implementation' in annotation
in annotation [io.swagger.v3.oas.annotations.media.Schema] which is not meta-present.
*/
  @AliasFor(annotation = Schema.class, attribute = "implementation")
  Class<?> schemaClass() default Void.class;
}
```

# Controller:
```java
@DefaultDocs(value = "Login", schemaClass = ExampleClass.class)
@PostMapping("/example")
  public ResponseEntity<ExampleClass> example(
    @RequestBody ExampleClass request
  ) throws HttpErrorException, DisabledException, BadCredentialsException {
    ExampleClass response = service.login(request, false);
    return ResponseEntity.ok(response);
  }
```
