 ```bash
 function whoami() {
   printf "%s\n" "${@}" || return $?;
 }

 whoami "developer, gamer, hobbyist, etc";
 ```
