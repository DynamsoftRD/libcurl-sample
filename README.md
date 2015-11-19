# How to Build and Use Libcurl
Libcurl is a free, open source library for transferring data. It supports various protocols include FTP, FTPS, HTTP, HTTPS, GOPHER, TFTP, SCP, SFTP, TELNET, DICT, LDAP, LDAPS, FILE, IMAP, SMTP, POP3, RTSP and RTMP.

How to Build libcurl with Visual Studio 2015 on Windows
-------------------------------------------------------
1. Download [libcurl][1].
2. Unzip the package and run **Visual Studio Command Line Tool**.
![Visual Studio 2015 command line tool](http://www.codepool.biz/wp-content/uploads/2015/11/vs_command_line.png)
3. Change directory to **winbuild**.
4. Build static libraries with following command:

   ```
   nmake /f Makefile.vc mode=static VC=14 MACHINE=x64 DEBUG=no
   ```
5. The generated libraries and header files are located at **../builds**.
![static libcurl](http://www.codepool.biz/wp-content/uploads/2015/11/libcurl_build.png)
6. Create a new win32 project in Visual Studio 2015.
7. Copy relevant libs and includes to the project.
8. Write a simple test.

    ```
    #include "stdafx.h"
    #include "libcurl/include/curl/curl.h"
    #ifdef _DEBUG
#pragma comment(lib, "libcurl/lib/libcurl_a_debug.lib")
#else
#pragma comment(lib, "libcurl/lib/libcurl_a.lib")
#endif
int main()
{
	curl_global_init(CURL_GLOBAL_DEFAULT);
	CURL *curl = curl_easy_init();
	if (curl) {
		CURLcode res;
		curl_easy_setopt(curl, CURLOPT_URL, "http://www.dynamsoft.com");
		res = curl_easy_perform(curl);
		curl_easy_cleanup(curl);
	}
	curl_global_cleanup();
    return 0;
}
    ```

References
---------
* https://github.com/bagder/curl
* http://curl.haxx.se/libcurl/c/libcurl-tutorial.html

Blog
----
[How to Build and Use Libcurl with VS2015 on Windows][2]

[1]:http://curl.haxx.se/download.html
[2]:http://www.codepool.biz/build-use-libcurl-vs2015-windows.html
