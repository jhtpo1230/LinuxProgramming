#include <sys/types.h>
#include <sys/stat.h>
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <string.h>
#include <time.h>
#include <limits.h>
#define sizeNum 30
void subDir(char *path);

void DirName() { // <함수1 - DirName : LS>
	DIR *dp;
	struct dirent *dent;

	dp = opendir(".");
	
	int j = 0;	
	while((dent = readdir(dp))) {
		if (dent->d_name[0] == '.') continue;
		else {
			printf("%s ", dent ->d_name);
                	j++;
                	if(j % 4 == 0) printf("\n");
		}
	}
	printf("\n");
	closedir(dp);
}

void DirIntro() { // <함수2 - DirIntro : LS -l>
	DIR *dp;
	struct dirent *dent;

	dp = opendir(".");
	while((dent = readdir(dp))) {
                if (dent->d_name[0] == '.') continue;
                else {
                	struct stat statbuf;
			stat(dent->d_name, &statbuf);

			int kind = statbuf.st_mode & S_IFMT;
        		switch(kind) {
                		case S_IFREG:
                        		printf("-");
                       			break;
               			case S_IFDIR:
                       			printf("d");
                       			break;
               			case S_IFLNK:
                       			printf("l");
                       			break;
                                case S_IFCHR:
                                        printf("c");
                                        break;
                                case S_IFBLK:
                                        printf("b");
                                        break;
                                case S_IFSOCK:
                                        printf("s");
                                        break;
                                case S_IFIFO:
                                        printf("p");
                                        break;
       			}
			if((statbuf.st_mode & S_IRUSR) != 0) printf("r");
			else printf("-");
			if((statbuf.st_mode & S_IWUSR) != 0) printf("w");
                        else printf("-");
                        if((statbuf.st_mode & S_IXUSR) != 0) printf("x");
                        else printf("-");
                        if((statbuf.st_mode & S_IRGRP) != 0) printf("r");
                        else printf("-");
                        if((statbuf.st_mode & S_IWGRP) != 0) printf("w");
                        else printf("-");
                        if((statbuf.st_mode & S_IXGRP) != 0) printf("x");
                        else printf("-");
                        if((statbuf.st_mode & S_IROTH) != 0) printf("r");
                        else printf("-");
                        if((statbuf.st_mode & S_IWOTH) != 0) printf("w");
                        else printf("-");
                        if((statbuf.st_mode & S_IXOTH) != 0) printf("x");
                        else printf("-");
			printf(" ");

                        printf("%o ", (unsigned int)statbuf.st_nlink);
                        printf("%d ", (unsigned int)statbuf.st_uid);
                        printf("%d ", (int)statbuf.st_gid);
                        printf("%d ", (int)statbuf.st_size);
			struct tm *t;
			t = localtime(&statbuf.st_mtime);
			printf("%d월 %d일 %d:%d " , t->tm_mon+1, t->tm_mday, t->tm_hour, t->tm_min);
			
	
                        printf("%s ", dent ->d_name);
                }
		printf("\n");
        }
	closedir(dp);

}
int num = 0;
void sizeRt() { // <함수 3 - sizeRt : LS -s 500>
        DIR *dp;
        struct dirent *dent;

        dp = opendir(".");

        int j = 0;
        int count = 0;
        int size[sizeNum] = {0};
	int nodeNum[sizeNum] = {0};

        while((dent = readdir(dp))) {
                if (dent->d_name[0] == '.') continue;
                else {
			struct stat statbuf;
                        stat(dent->d_name, &statbuf);

			if (((int)statbuf.st_size) >= 500) {
				num++;
                                size[count] = statbuf.st_size;
				nodeNum[count] = dent->d_ino;
				count++;
			}			
                }
        }
	int x, y, temp, temp2;
	for(x=1; x<num; x++) {
		for(y=0; y<=x; y++) {
			if (size[y] <= size[x]) {
				temp = size[x];
				temp2 = nodeNum[x];	
				size[x] = size[y];
				nodeNum[x] = nodeNum[y];
				size[y] = temp;
				nodeNum[y] = temp2;
			}
		}
	}
	rewinddir(dp);
	int i=0;

	for(i=0; i<num; i++) {
	        while((dent = readdir(dp))) {
                        struct stat statbuf;
                        stat(dent->d_name, &statbuf);

        	        if (dent->d_name[0] == '.') continue;
                	else {
				if(nodeNum[i] == (dent->d_ino)) {
					printf("%s", dent->d_name);
					printf("(%d) ", (int)statbuf.st_size);
					j++;
					if (j % 4 == 0) printf("\n");
				}
			}	
		}
		rewinddir(dp);
	}
        printf("\n");
        closedir(dp);
}

void sizeRtAll() { // <함수 4 - sizeRtAll : LS -ls 500>
        DIR *dp;
        struct dirent *dent;

        dp = opendir(".");

        int j = 0;
        int count = 0;
        int size[sizeNum] = {0};
        int nodeNum[sizeNum] = {0};

        while((dent = readdir(dp))) {
                if (dent->d_name[0] == '.') continue;
                else {
                        struct stat statbuf;
                        stat(dent->d_name, &statbuf);

                        if (((int)statbuf.st_size) >= 500) {
				num++;
                                size[count] = statbuf.st_size;
                                nodeNum[count] = dent->d_ino;
                                count++;
                        }
                }
        }
        int x, y, temp, temp2;
        for(x=1; x<num; x++) {
                for(y=0; y<=x; y++) {
                        if (size[y] <= size[x]) {
                                temp = size[x];
                                temp2 = nodeNum[x];
                                size[x] = size[y];
                                nodeNum[x] = nodeNum[y];
                                size[y] = temp;
                                nodeNum[y] = temp2;
                        }
                }
        }
        rewinddir(dp);
        int i=0;
        for(i=0; i<num; i++) {
                while((dent = readdir(dp))) {
                        struct stat statbuf;
                        stat(dent->d_name, &statbuf);

                        if (dent->d_name[0] == '.') continue;
                        else {
                                if(nodeNum[i] == (dent->d_ino)) {
		                        int kind = statbuf.st_mode & S_IFMT;
                		        switch(kind) {
                                		case S_IFREG:
                                        		printf("-");
                                        		break;
                               		 	case S_IFDIR:
                                        		printf("d");
                                       			break;
                               			case S_IFLNK:
                               			        printf("l");
                                       			break;
                                		case S_IFCHR:
                                        		printf("c");
                                        		break;
		                                case S_IFBLK:
                		                        printf("b");
                               			        break;
                                		case S_IFSOCK:
                                        		printf("s");
                                        		break;
                                		case S_IFIFO:
                                        		printf("p");
                                       			break;
                        		}
					if((statbuf.st_mode & S_IRUSR) != 0) printf("r");
                        		else printf("-");
                        		if((statbuf.st_mode & S_IWUSR) != 0) printf("w");
                        		else printf("-");
                        		if((statbuf.st_mode & S_IXUSR) != 0) printf("x");
                        		else printf("-");
                        		if((statbuf.st_mode & S_IRGRP) != 0) printf("r");
                        		else printf("-");
                        		if((statbuf.st_mode & S_IWGRP) != 0) printf("w");
                        		else printf("-");
                        		if((statbuf.st_mode & S_IXGRP) != 0) printf("x");
                        		else printf("-");
                        		if((statbuf.st_mode & S_IROTH) != 0) printf("r");
                        		else printf("-");
                       			if((statbuf.st_mode & S_IWOTH) != 0) printf("w");
                        		else printf("-");
                        		if((statbuf.st_mode & S_IXOTH) != 0) printf("x");
                        		else printf("-");
                        		printf(" ");
                 
				        printf("%o ", (unsigned int)statbuf.st_nlink);
                        		printf("%d ", (unsigned int)statbuf.st_uid);
                        		printf("%d ", (int)statbuf.st_gid);
                        		printf("%d ", (int)statbuf.st_size);
                        		struct tm *t;
                        		t = localtime(&statbuf.st_mtime);
                        		printf("%d월 %d일 %d:%d " , t->tm_mon+1, t->tm_mday, t->tm_hour, t->tm_min);
		

                		        printf("%s ", dent ->d_name);
                        		printf("\n");
                        		}
           			}
		}
                rewinddir(dp);
        }
        printf("\n");
        closedir(dp);
}

void prinDir() { // <함수 5 - printDir : LS -F>
        DIR *dp;
        struct dirent *dent;

        dp = opendir(".");

        int j = 0;
        while((dent = readdir(dp))) {
                if (dent->d_name[0] == '.') continue;
                else {
                        struct stat statbuf;
                        stat(dent->d_name, &statbuf);

                        int kind = statbuf.st_mode & S_IFMT;

			if(kind != S_IFDIR) {
				if((statbuf.st_mode & S_IXUSR) != 0 && (statbuf.st_mode & S_IXGRP) != 0 && (statbuf.st_mode & S_IXOTH) != 0 ) {
					printf("%s", dent ->d_name);
					printf("* ");
                        	}
				else {
	                                printf("%s ", dent ->d_name);
				}
			}
	                 else  {
                                printf("%s", dent ->d_name);
                                printf("/ ");
                         }
                        j++;
                        if(j % 4 == 0) printf("\n");
                }
        }
        printf("\n");
        closedir(dp);

}

void openSubDir(char *path) {
	DIR *dp;
	struct dirent *dent;
	
	dp = opendir(path);

	if(dp == NULL) {
                perror("None Dir");
	}
	else {
	while(dent = readdir(dp)) {
		struct stat statbuf;
		stat(dent->d_name, &statbuf);

                if (dent->d_name[0] == '.') continue;
                else if ((statbuf.st_mode & S_IFMT) != S_IFDIR) continue;
                else {
	                char pathDir[PATH_MAX];
                	sprintf(pathDir, "%s/%s",path,dent->d_name);
                	printf("Current Dir : %s\n",pathDir);
			subDir(pathDir);
		}
	}
	rewinddir(dp);
	}

	closedir(dp);
}

void subDir(char *path) {
        DIR *dp;
        struct dirent *dent;

        dp = opendir(path);

        if(dp == NULL) {
		perror("None Dir");
        }
	else {
        while(dent = readdir(dp)) {
                struct stat statbuf;
                stat(dent->d_name, &statbuf);

                if (dent->d_name[0] == '.') continue;
                else {
                        char pathDir[PATH_MAX];
                        sprintf(pathDir, "%s/%s",path,dent->d_name);
                        printf("Current Dir : %s\n",pathDir);
			subDir(pathDir);
                }
        }
        rewinddir(dp);
	}
        printf("\n");
        closedir(dp);

}

void prinSub() { // <함수 6 - prinSub : LS -R>
        DIR *dp;
        struct dirent *dent;

        dp = opendir(".");

        char path[PATH_MAX];
        if (getcwd(path, PATH_MAX)==NULL) {
		perror("getcwd error");
		exit(EXIT_FAILURE);
	}
        else {
		printf("Current Dir : %s\n",path);
		prinDir();
		printf("\n");
        	openSubDir(path);
        }

        closedir(dp);
}

void prinRever() { // <함수 7 - prinRever : LS -r>
        if(
	rewinddir(dp);

        while((dent = readdir(dp))) {
                if (dent->d_name[0] == '.') continue;
		else if (91 >= dent->d_name[0] && dent->d_name[0] >= 65)
			continue;
                else if (122 >= dent->d_name[0] && dent->d_name[0] >= 97)
			continue;
                else {
                	printf("%s\n", dent->d_name);
                }
        }
        rewinddir(dp);
	
	char ch1, ch2;
	int j = 0;
        for(ch2=122; ch2>=97; ch2--) {
                while((dent = readdir(dp))) {
                        if (dent->d_name[0] == '.') continue;
                        else {
                                if (dent->d_name[0] == ch2) {
                                        printf("%s ",dent->d_name);
					j++;
					if (j % 4 == 0) printf("\n");
                                }
                        }
                }
                rewinddir(dp);
        }
	for(ch1=90; ch1>=65; ch1--) {
		while((dent = readdir(dp))) {
                	if (dent->d_name[0] == '.') continue;
                	else {
				if (dent->d_name[0] == ch1) {
					printf("%s ",dent->d_name);
					j++;
					if(j % 4 == 0) printf("\n");
				}
                	}
			
        	}
        	rewinddir(dp);
	}
        closedir(dp);
}

int main(int argc, char *argv[]) {
	if (argc == 1 && argc < 2) {
		DirName();
	}
	else if (argc == 2) {
		if (strcmp(argv[1], "-l") == 0) {
			DirIntro();
		}
		else if (strcmp(argv[1], "-F") == 0) {
			prinDir();
		}
		else if (strcmp(argv[1], "-R") == 0) {
			prinSub();
		}
		else if (strcmp(argv[1], "-r") == 0) {
			prinRever();
                }
			
	}
	else if (argc == 3) {
		if (strcmp(argv[1], "-s") == 0 && strcmp(argv[2], "500") == 0) {
			sizeRt();
                }
		else if (strcmp(argv[1], "-ls") == 0 && strcmp(argv[2], "500") == 0) {
			sizeRtAll();
		}
                else if (strcmp(argv[1], "-d") == 0 && strcmp(argv[2], "-l") == 0) {
                        prinDir();
                }

	}
	else if (argc == 4) {
		sizeRtAll();	
	}
	return 0;
}
