CC ?= gcc
OPT = -O2 -g
CFLAGS = $(OPT) $(INCFLAGS) -Wall -Wextra -Wno-parentheses -std=gnu99
INCFLAGS = -I../../lib/igb -I../../daemons/mrpd -I../common -I../../lib/common -I../../daemons/common
LDLIBS = -ligb -lpci -lrt -pthread -ljack
LDFLAGS = -L../../lib/igb

all: jackd_talker

jackd_talker: jackd_talker.o jack.o ../common/talker_mrp_client.o ../../lib/common/avb.o

jack.o: jack.c jack.h defines.h
	$(CC) $(CFLAGS) -c jack.c

jackd_talker.o: jackd_talker.c defines.h jack.h
	$(CC) -c $(INCFLAGS) -I../../daemons/mrpd $(CFLAGS) jackd_talker.c

../../lib/common/avb.o: ../../lib/common/avb.c ../../lib/common/avb.h
	make -C ../../lib/common/ avb.o

../common/talker_mrp_client.o:
	make -C ../common/ talker_mrp_client.o

%: %.o
	$(CC) $(LDFLAGS) $^ $(LDLIBS) -o $@

clean:
	$(RM) jackd_talker
	$(RM) `find . -name "*~" -o -name "*.[oa]" -o -name "\#*\#" -o -name TAGS -o -name core -o -name "*.orig"`
