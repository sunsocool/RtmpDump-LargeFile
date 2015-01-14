# RtmpDump-LargeFile-BugFix
RtmpDump Version 2.4 Large File BugFix. "Unexpected start of file, error in tag sizes, couldn't arrive at prevTagSize=0"

  When I using youtube-dl to download some video from website,I found that When the video file is very large like 4.48GB. RtmpDump will report error "ERROR: Unexpected start of file, error in tag sizes, couldn't arrive at prevTagSize=0" 
  
  So I download the source file,try and try again finally the project works, and then check and check again ... At last I figure out what's wrong with the program. In the last version seems trying to fix the large file problem using  ftello instead of ftell .But the fseek function remains the same ,when execute   fseek(file, 0, SEEK_END);   size = ftello(file);  Actually  ftello(file) returns 0 to size.Finally I figure out the bug is that replace all fseek with fseeko to deal with large file problem.
  
  Thanks for RtmpDump team proving this wonderful software stack.
