# Question

Is KAN GPU friendly? Can we investigate some of the OOMs found in 
https://github.com/Blealtan/efficient-kan/issues/23
https://github.com/Blealtan/efficient-kan/issues/24

# TODO
(Should probably get flame charts for all of these)
[ ] Profile this as is
[ ] Profile this with all tensors gpu'd

# Current ideas
If there is a problem flash attention maybe the easiest lift. Lets find out
