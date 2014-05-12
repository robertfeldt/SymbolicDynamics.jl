#####################################################################
# Constants
#####################################################################
Lib = "SymbolicDynamics"

Julia = "julia"
# Julia = "julia03"


#####################################################################
# Tasks
#####################################################################
desc "Run normal (fast) tests"
task :runtest do
  if File.exist?("test/runtests.jl")
    sh "#{Julia} -L src/#{Lib}.jl test/runtests.jl"
  end
end

desc "Run slow tests"
task :runslowtest do
  if File.exist?("test/runslowtests.jl")
    sh "#{Julia} -L src/#{Lib}.jl test/runslowtests.jl"
  end
end

desc "Run all tests"
task :runalltest => [:runtest, :runslowtest]

def filter_latest_changed_files(filenames, numLatestChangedToInclude = 1)
  filenames.sort_by{ |f| File.mtime(f) }[-numLatestChangedToInclude, numLatestChangedToInclude]
end

desc "Run only the latest changed test file"
task :t do
  latest_changed_test_files = filter_latest_changed_files Dir["test/**/test*.jl"]
  sh "#{Julia} -L src/BlackBoxOptim.jl -L test/helper.jl #{latest_changed_test_files.first}"
end

task :at => :runalltest
task :st => :runslowtest

task :default => :runtest