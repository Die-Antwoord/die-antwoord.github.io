<!DOCTYPE html>
<html>
<body>
    <div>
        <div>
            <div>
                <div>
                    <div>
                        <h1>AUTH2 URL PARSER</h1>
                    </div>
                </div>
            </div>
            <div class="container">
                <form>
                    <br />
                    <h4>
                        Enter URL
                    </h4>
                    <input id="url" class="inp" name="url" type="url" width="100%" />
                    <br />
                    <br />
                    <button ripple>
                        Parse!
                    </button>
                    <br />
                    <br />
                    <div style="font-weight: 600; font-size: 22px;">
                        ID: <id></id><br />
                        REDIRECT URI: <redirect_uri></redirect_uri><br />
                        SCOPE: <scope></scope>
                    </div>
                </form>
            </div>
        </div>
    </div>
</body>

</html>

<script>
    window.onload = () => {
        var params = new URLSearchParams(window.location.search);
        var url = decodeURI(params.get("url"));

        if (params.get("url") !== null) {
            var oauthParams = new URLSearchParams(new URL(url).search);

            document.querySelector("#url").value = url;

            if (url.includes("https://discord.com/api/oauth2/authorize") || url.includes("https://discord.com/oauth2/authorize")) {
                if (oauthParams.has("client_id") && oauthParams.has("redirect_uri") && oauthParams.has("scope")) {
                    document.querySelector("id").innerText = oauthParams.get("client_id");
                    document.querySelector("redirect_uri").innerHTML = `<a href="${decodeURI(oauthParams.get("redirect_uri"))}">` + decodeURI(oauthParams.get("redirect_uri")) + "</a>";
                    document.querySelector("scope").innerHTML = decodeURI(oauthParams.get("scope")).split(" ").join(", ");
                }
            }
        }
    };
</script>