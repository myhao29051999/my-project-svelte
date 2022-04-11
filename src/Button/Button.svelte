<script>
    export let key;
    export let result;
    const error = "Invalid input!";

    function replace(value) {
        return value.replace("x", "*").replace("÷", "/");
    }

    function handleClick(){
        switch (key) {
            case "=":
                try {
                    result = eval(replace(result));
                } catch (error) {
                    result = error;
                }
                break;
            case "C":
                result = "0";
                break;
            default:
                result = result === error || result === "0" ? key : result + key;
        }
    }
</script>
<button on:click={handleClick}>{key}</button>