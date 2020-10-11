# Kata-Extract-the-domain-name-from-a-URL

Write a function that when given a URL as a string, parses out just the domain name and returns it as a string. For example:

domainName("http://github.com/carbonfive/raygun") == "github" 

domainName("http://www.zombie-bites.com") == "zombie-bites"

domainName("https://www.cnet.com") == "cnet"








TESTS
------------------------------------------------------------------------------
Test.describe("Basic tests",function(){
Test.assertEquals(domainName("http://google.com"), "google");
Test.assertEquals(domainName("http://google.co.jp"), "google");
Test.assertEquals(domainName("https://123.net"), "123");
Test.assertEquals(domainName("https://hyphen-site.org"), "hyphen-site");
Test.assertEquals(domainName("http://codewars.com"), "codewars");
Test.assertEquals(domainName("www.xakep.ru"), "xakep");
Test.assertEquals(domainName("https://youtube.com"), "youtube");
Test.assertEquals(domainName("http://www.codewars.com/kata/"), "codewars");
Test.assertEquals(domainName("icann.org"), "icann");
})

Test.describe("Random tests",function(){
  prefixes=["","http://","https://","http://www.","https://www."]
  base="0123456789abcdefghijklmnopqrstuvwxyz-"
  secondlevel=[".com",".co.uk",".net",".edu",".co.za",".it",".org",".biz",".fr",".de",".jp",".br",".tv",".co",".tv",".pro",".name",".us",".info",".io"]
  randomstuff=["","","/","/img/","/users","/default.html","/index.php","/warez/","/error","/archive/"]
  function randint(a,b){return Math.floor(Math.random()*(b-a+1))+a;}
  function domainSol(url){return url.replace("www.","").replace("https://","").replace("http://","").split(".")[0];}
  for (var _=0;_<40;_++){
    domainlength=randint(5,30)
    domain=""
    while(domainlength){
      nextletter=base[randint(0,36)]
      if (nextletter!="-" || (domainlength!=1 && domain!="")){
        domain+=nextletter;
        domainlength--;
      }
    }
    url=prefixes[randint(0,4)]+domain+secondlevel[randint(0,19)]+randomstuff[randint(0,9)];
    Test.it("Testing for "+url,function(){
      Test.assertEquals(domainName(url),domainSol(url),"It should work for random inputs too")
    })
  }
})
