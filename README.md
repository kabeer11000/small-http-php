# Small HTTP <small>-PHP</small>

Small HTTP Class to make HTTP-GET/POST/PUT/DELETE requests based on curl, concerning just about the response body.

## Improvements

Using http_build_query to get the query-string out of an request-array.(you could also use the array itself, 
therefore see: http://php.net/manual/en/function.curl-setopt.php)
Returning the response instead of echoing it. Btw you can avoid the returning by removing the line curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);. 
After that the return value is a boolean(true = request was successful otherwise an error occured) and the response is echoed. See: http://php.net/en/manual/function.curl-exec.php

Clean session closing and deletion of the curl-handler by using curl_close. See: http://php.net/manual/en/function.curl-close.php

Using boolean values for the curl_setopt function instead of using any number.
(I know that any number not equal zero is also considered as true, but the usage of true generates a more readable code, but that's just my opinion)
Ability to make HTTP-PUT/DELETE calls(useful for RESTful service testing)


## Example Usage

### GET

```
$response = SmallHttp::HTTPGet("http://localhost/service/foobar.php", array("getParam" => "foobar"));
```

### POST

```
$response = SmallHttp::HTTPPost("http://localhost/service/foobar.php", array("postParam" => "foobar"));
```

### PUT

```
$response = SmallHttp::HTTPPut("http://localhost/service/foobar.php", array("putParam" => "foobar"));
```

### DELETE

```
$response = SmallHttp::HTTPDelete("http://localhost/service/foobar.php", array("deleteParam" => "foobar"));
```

## TESTING

You can also make some cool service tests by using this simple class.
```
class SmallHttpCase extends TestCase {
    /**
     * @description test static method HTTPGet
     */
    public function testHTTPGet() {
        $requestArr = array("getLicenses" => 1);
        $url        = "http://localhost/project/req/licenseService.php";
        $this->assertEquals(SmallHttp::HTTPGet($url, $requestArr), '[{"error":false,"val":["NONE","AGPL","GPLv3"]}]');
    }
    /**
     * @description test static method HTTPPost
     */
    public function testHTTPPost() {
        $requestArr = array("addPerson" => array("foo", "bar"));
        $url        = "http://localhost/project/req/personService.php";
        $this->assertEquals(SmallHttp::HTTPPost($url, $requestArr), '[{"error":false}]');
    }
    /**
     * @description test static method HTTPPut
     */
    public function testHTTPPut() {
        $requestArr = array("updatePerson" => array("foo", "bar"));
        $url        = "http://localhost/project/req/personService.php";
        $this->assertEquals(SmallHttp::HTTPPut($url, $requestArr), '[{"error":false}]');
    }
    /**
     * @description test static method HTTPDelete
     */
    public function testHTTPDelete() {
        $requestArr = array("deletePerson" => array("foo", "bar"));
        $url        = "http://localhost/project/req/personService.php";
        $this->assertEquals(SmallHttp::HTTPDelete($url, $requestArr), '[{"error":false}]');
    }
}

```

By Kabeers Network - Helpful things that make life radically easier.
