# Result.java

```
public class Result<Ok, Error> {
    @Nullable
    Ok value;
    @Nullable
    Error error;
    boolean success;

    private Result(@Nullable Ok value, @Nullable Error error, boolean success) {
        this.value = value;
        this.error = error;
        this.success = success;
    }

    public static <Ok, Error> Result<Ok, Error> ofSuccess(@NotNull Ok value) {
        return new Result<>(value, null, true);
    }

    public static <Ok, Error> Result<Ok, Error> ofError(@NotNull Error error) {
        return new Result<>(null, error, false);
    }

    public Optional<Ok> peekOk() {
        return Optional.ofNullable(value);
    }

    public Optional<Ok> peekError() {
        return Optional.ofNullable(value);
    }

    public boolean ifOk(Consumer<Ok> c) {
        if (value != null) {
            c.accept(value);
            return true;
        }
        return false;
    }

    public boolean ifError(Consumer<Error> c) {
        if (error != null) {
            c.accept(error);
            return true;
        }
        return false;
    }

    public boolean take(Consumer<Ok> kk, Consumer<Error> err) {
        if (value != null) {
            kk.accept(value);
            return true;
        }
        err.accept(error);

        return false;
    }

    public boolean isOk() {
        return value != null;
    }

    public boolean isError() {
        return error != null;
    }
}
```
