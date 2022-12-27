# Cloud Functions example
- API https://cloud.google.com/functions/docs/writing/write-http-functions#http-example-java
- HttpRequest - https://javadoc.io/doc/com.google.cloud.functions/functions-framework-api/latest/com/google/cloud/functions/HttpRequest.html
- see https://developers.googleblog.com/2020/05/java-11-for-cloud-functions.html
- https://cloud.google.com/docs/samples?language=java&product=cloudfunctions
- CORS https://cloud.google.com/functions/docs/samples/functions-http-cors?hl=en
## Random function
Location: ol.dev : was kcc-lz-nnnn - now eventstream.dev
https://random2-hjcikuu52q-nn.a.run.app/?list=first,second,third,forth
not
https://random-3qd3vhjyca-nn.a.run.app/?list=first,second,third,forth


## Code : Java 17: Gen 2

```
package gcfv2;

import java.io.BufferedWriter;
import java.io.IOException;

import com.google.cloud.functions.HttpFunction;
import com.google.cloud.functions.HttpRequest;
import com.google.cloud.functions.HttpResponse;

import java.util.Collections;
import java.util.List;
import java.util.Optional;
import java.util.StringTokenizer;
import java.util.stream.Collectors;


public class HelloHttpFunction implements HttpFunction {

  public String random(BufferedWriter writer, String input) throws java.lang.Exception {
		List<String> strings = Collections.list(new StringTokenizer(input, ",")).stream()
	      .map(token -> (String) token)
	      .collect(Collectors.toList());
    int index = (int)(Math.random() * strings.size());
    writer.write("{key: " + index + ", ");
		return strings.get(index);
  }

  public void service(final HttpRequest request, final HttpResponse response) throws java.lang.Exception, IOException {
    final BufferedWriter writer = response.getWriter();
    Optional<String> aCSVString = aCSVString = request.getFirstQueryParameter("list");
    if(aCSVString.isPresent()) {
      writer.write("value: " + random(writer, aCSVString.get()) + "}");
    } else {
      writer.write("append ?list=first,second,third....to get a random indexed string back in json");
    }
  }
}
```

accidentally deleted
https://console.cloud.google.com/functions/details/northamerica-northeast1/random?env=gen2&project=net-host-prj-nonprod-oldv2
