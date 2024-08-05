# Define the path to the kernel source
kernel_include = include_directories('/arch/x86/virt/vmx/tdx/')

i386_kvm_ss = ss.source_set()

i386_kvm_ss.add(files(
  'kvm.c',
  'kvm-cpu.c',
))

i386_kvm_ss.add(when: 'CONFIG_XEN_EMU', if_true: files('xen-emu.c'))

i386_kvm_ss.add(when: 'CONFIG_TDX', if_true: files('tdx.c', 'tdx-quote-generator.c'), if_false: files('tdx-stub.c'))

i386_system_ss.add(when: 'CONFIG_HYPERV', if_true: files('hyperv.c'), if_false: files('hyperv-stub.c'))

# Add the include directory to the source set
i386_kvm_ss.include_directories(kernel_include)

i386_system_ss.add_all(when: 'CONFIG_KVM', if_true: i386_kvm_ss)
