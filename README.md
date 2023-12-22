# DailyOutput_TauxTauy_SurfUV_CESM1

This directory provides modified source code files for CESM 1.2.2.1 to implement daily output of a select few POP2 ocean history fields while otherwise maintaining monthly averaging for the rest. 

Unlike CAM, history fields in POP2 can only be output at one time-averaging frequency (e.g., monthly, daily, etc.). By default, POP2 outputs most things monthly. You can easily change the time averaging frequency of the main output stream to daily, but this then changes all of the variables within that time-averaging stream to daily output. This is a large amount of storage. Another wrinkle to this issue is that separating some variables off from the main time averaging stream can lead the model to crash during the time-averaging step. This means, for instance, you can't/shouldn't put a major variable onto a secondary time-averaging stream from the primary time-averaging stream unless you're sure the model won't crash from this choice. 

To work around this, in Luongo et al. (In Review) I modified forcing.F90 to allocate two new variables, TAUX_2 and TAUY_2, and added them to gx1vg_tavg_contents in the daily averaging stream. These variables are the exact same thing as TAUX and TAUY but have a different name to avoid runtime crashes.

I also output U1_1 and V1_1, surface UVEL and VVEL, at daily resolution by adding these two variables to gx1v6_tavg_contents daily stream. These variables were pre-allocated within baroclinic.F90 but are not usually output. 

I found this blog post helpful: https://bb.cgd.ucar.edu/cesm/threads/pop2-daily-ocean-temperature-output.3172/#post-13975
As well as the POP2 manual section on time-averaging: https://www2.cesm.ucar.edu/models/cesm1.2/pop2/doc/faq/#developer

To see my edits, search "luongo" in the .F90 file. Please reach out to me at mluongo(at)ucsd(dot)edu if you have any questions about these code modifications or the workflow.

Matt Luongo

Scripps Institution of Oceanography, UCSD

La Jolla, CA, USA

December 2023



