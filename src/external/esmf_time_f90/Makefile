.SUFFIXES: .F90 .o

OBJS = ESMF_AlarmClockMod.o \
	   ESMF_AlarmMod.o \
	   ESMF_BaseMod.o \
	   ESMF_BaseTimeMod.o \
	   ESMF_CalendarMod.o \
	   ESMF_ClockMod.o \
	   ESMF.o \
	   ESMF_FractionMod.o \
	   ESMF_ShrTimeMod.o \
	   ESMF_Stubs.o \
	   ESMF_TimeIntervalMod.o \
	   ESMF_TimeMod.o \
	   MeatMod.o \
	   wrf_error_fatal.o \
	   wrf_message.o

all: $(OBJS)
	ar -ru libesmf_time.a *.o

ESMF_AlarmClockMod.o: ESMF_AlarmMod.o ESMF_ClockMod.o ESMF_TimeIntervalMod.o ESMF_TimeMod.o

ESMF_AlarmMod.o: ESMF_BaseMod.o ESMF_TimeIntervalMod.o ESMF_TimeMod.o

ESMF_BaseMod.o:

ESMF_BaseTimeMod.o: ESMF_BaseMod.o

ESMF_CalendarMod.o: ESMF_BaseMod.o ESMF_BaseTimeMod.o

ESMF_ClockMod.o: ESMF_BaseMod.o ESMF_TimeIntervalMod.o ESMF_TimeMod.o ESMF_AlarmMod.o ESMF_TimeMod.o

ESMF.o: ESMF_AlarmMod.o ESMF_BaseMod.o ESMF_BaseTimeMod.o \
		ESMF_CalendarMod.o ESMF_ClockMod.o ESMF_FractionMod.o \
		ESMF_TimeIntervalMod.o ESMF_TimeMod.o ESMF_ShrTimeMod.o \
		ESMF_AlarmClockMod.o ESMF_Stubs.o MeatMod.o

ESMF_FractionMod.o:

ESMF_ShrTimeMod.o: ESMF_BaseMod.o ESMF_BaseTimeMod.o ESMF_CalendarMod.o

ESMF_Stubs.o: ESMF_BaseMod.o ESMF_CalendarMod.o

ESMF_TimeIntervalMod.o: ESMF_BaseMod.o ESMF_BaseTimeMod.o ESMF_FractionMod.o ESMF_CalendarMod.o ESMF_ShrTimeMod.o

ESMF_TimeMod.o: ESMF_BaseMod.o ESMF_BaseTimeMod.o ESMF_TimeIntervalMod.o ESMF_CalendarMod.o ESMF_ShrTimeMod.o ESMF_Stubs.o

MeatMod.o: ESMF_BaseMod.o

wrf_error_fatal.o:

wrf_message.o:

clean:
	rm -rf *.tmp.f90 *.o *.mod *.a

.F90.o:
	$(RM) $@ $*.mod
ifeq "$(GEN_F90)" "true"
	$(CPP) $(CPPFLAGS) $< > $*.tmp.f90 $(CPPINCLUDES) $(FCINCLUDES) -I.
	$(FC) $(FFLAGS) -c $*.tmp.f90 $(CPPINCLUDES) $(FCINCLUDES) -I.
else
	$(FC) $(CPPFLAGS) $(FFLAGS) -c $*.F90 $(CPPINCLUDES) $(FCINCLUDES) -I.
endif
