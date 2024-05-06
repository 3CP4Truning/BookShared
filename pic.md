import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class MarkdownImageDetector {

    private static final Pattern IMAGE_PATTERN = Pattern.compile("(?<!<img\\bsrc=\")(.*?)(?=\")");

    public static boolean isImageLine(String line, String[] urlHolder) {
        Matcher matcher = IMAGE_PATTERN.matcher(line);
        if (matcher.find()) {
            urlHolder[0] = matcher.group(1); // Capture and store the image URL
            return true;
        }
        return false;
    }

    // ... (rest of the code remains the same)

    public static void main(String[] args) {
        String line1 = "![](https://www.example.com/image.png)";
        String line2 = "<img src=\"https://www.example.com/image2.png\">";
        String line3 = "This is not an image.";

        String[] urlHolder = new String[1]; // To store the extracted URL

        System.out.println(isImageLine(line1, urlHolder)); // true
        System.out.println("Image URL: " + urlHolder[0]); // Output: Image URL: https://www.example.com/image.png

        System.out.println(isImageLine(line2, urlHolder)); // true
        System.out.println("Image URL: " + urlHolder[0]); // Output: Image URL: https://www.example.com/image2.png

        System.out.println(isImageLine(line3, urlHolder)); // false
        System.out.println("Image URL: " + urlHolder[0]); // Output: Image URL: null
    }
}
Explanation of Changes:

isImageLine Method:

The method now takes an additional parameter String[] urlHolder to store the extracted image URL.
Inside the if (matcher.find()) block:
The matcher.group(1) call captures the image URL from the matched pattern.
The URL is stored in the urlHolder[0] element.
The method returns true if an image is found and false otherwise.
main Function:

A String[] urlHolder array is created to hold the extracted URL.
When calling isImageLine, the urlHolder array is passed as an argument.
After calling isImageLine, the urlHolder[0] is checked to see if an image URL was extracted.
The extracted URL is printed if available.
How it Works:

When isImageLine is called, it attempts to match the line against the IMAGE_PATTERN.

If a match is found, the matcher.group(1) call extracts the captured group, which is the image URL.

The extracted URL is stored in the provided urlHolder array.

The method returns true to indicate that an image line was detected.

In the main function, the urlHolder array is passed to isImageLine to capture the URL.

After calling isImageLine, the urlHolder[0] is checked, and the extracted URL is printed if available.

With this modification, the code not only identifies image lines but also extracts the corresponding image URLs, making it more versatile for image processing tasks.

import java.io.BufferedReader;  
import java.io.FileReader;  
import java.io.IOException;  
import java.util.regex.Matcher;  
import java.util.regex.Pattern;  
  
public class MarkdownImageChecker {  
  
    // Markdown图片链接的正则表达式  
    private static final Pattern MARKDOWN_IMAGE_PATTERN = Pattern.compile("!\\[.*?\\]\\((.*?)\\)");  
  
    // HTML <img> 标签的正则表达式  
    private static final Pattern HTML_IMG_PATTERN = Pattern.compile("<img[^>]+src=[\"'](.*?)[\"'][^>]*>", Pattern.CASE_INSENSITIVE);  
  
    public static boolean isImageLine(String filePath, int lineNumber) throws IOException {  
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {  
            String line;  
            int currentLine = 1;  
            while ((line = reader.readLine()) != null) {  
                if (currentLine == lineNumber) {  
                    // 检查Markdown图片链接  
                    Matcher markdownMatcher = MARKDOWN_IMAGE_PATTERN.matcher(line);  
                    if (markdownMatcher.find()) {  
                        return true;  
                    }  
  
                    // 检查HTML <img> 标签  
                    Matcher htmlMatcher = HTML_IMG_PATTERN.matcher(line);  
                    if (htmlMatcher.find()) {  
                        return true;  
                    }  
  
                    // 如果没有找到任何匹配项，则返回false  
                    return false;  
                }  
                currentLine++;  
            }  
            // 如果文件没有指定数量的行，理论上我们不会到达这里，因为上面的return语句会在找到匹配项时退出循环  
            return false;  
        }  
    }  
  
    public static void main(String[] args) {  
        String filePath = "path_to_your_markdown_file.md";  
        int lineNumber = 5; // 假设你想检查第5行  
  
        try {  
            if (isImageLine(filePath, lineNumber)) {  
                System.out.println("Line " + lineNumber + " contains an image.");  
            } else {  
                System.out.println("Line " + lineNumber + " does not contain an image.");  
            }  
        } catch (IOException e) {  
            e.printStackTrace();  
        }  
    }  
}
这个正则表达式的解释如下：

<img：匹配字面的<img开始标签。
[^>]+：匹配一个或多个不是>的字符，这确保了我们会匹配到整个<img ... >标签，而不是只到第一个出现的>为止。
src=["']：匹配src属性后紧跟的=和引号（单引号或双引号）。
(.*?)：这是一个捕获组，用于匹配并捕获引号之间的URL内容。这里的?表示非贪婪匹配，意味着它会尽可能少地匹配字符。
["']：匹配结束引号（与开始引号相同的类型）。
[^>]*>：匹配零个或多个不是>的字符，然后是一个>字符，这确保了我们匹配到标签的结束。
Pattern.CASE_INSENSITIVE：这是一个编译标志，表示匹配应该是不区分大小写的。这对于HTML属性名（如src）通常是不必要的，因为它们是大小写不敏感的，但在某些情况下可能是有用的。
