#include <stdio.h>
#include <stdbool.h>

struct exploitable {
	char buf[10];
	bool p0wned;
	int  num;
};

int main(void) {
	struct exploitable ex;
	for (int i = 0; i < 9; i++) {
		ex.buf[i] = 'a';
	}
	ex.buf[9] = '\0';
	
	ex.p0wned = false;
	ex.buf[10] = '\1';

	ex.num = 42;
	/*for (int i = 10; i < 20; i++) {
		ex.buf[i] = '\1';
	}*/
	ex.buf[11] = 0;
	ex.buf[12] = 0;
	ex.buf[13] = 0;

	printf("'%s' %s %i %x (%i)\n", ex.buf,
			(ex.p0wned ? "p0wned" : "whee!"),
			ex.num, ex.num, sizeof(ex.num));

	return 0;
}
