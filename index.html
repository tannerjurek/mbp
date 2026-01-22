import React, { useState, useEffect } from 'react';
import { Trash2, Plus, TrendingUp, X, Check } from 'lucide-react';
import { LineChart, Line, BarChart, Bar, PieChart, Pie, Cell, XAxis, YAxis, CartesianGrid, Tooltip, Legend, ResponsiveContainer } from 'recharts';

const MBP_GRADES = [
  { grade: 'V0', color: '#F4E03C', textColor: '#000', value: 0 },
  { grade: 'V0-V2', color: '#DC143C', textColor: '#fff', value: 1 },
  { grade: 'V1-V3', color: '#2D5D3B', textColor: '#fff', value: 2 },
  { grade: 'V2-V4', color: '#4A148C', textColor: '#fff', value: 3 },
  { grade: 'V3-V5', color: '#D2691E', textColor: '#fff', value: 4 },
  { grade: 'V4-V6', color: '#000000', textColor: '#fff', value: 5 },
  { grade: 'V5-V7', color: '#1E90FF', textColor: '#fff', value: 6 },
  { grade: 'V6-V8', color: '#C71585', textColor: '#fff', value: 7 },
  { grade: 'V8-V10+', color: '#FFFFFF', textColor: '#000', value: 8 }
];

export default function BoulderingTracker() {
  const [boulders, setBoulders] = useState([]);
  const [view, setView] = useState('projects');
  const [focusedBoulder, setFocusedBoulder] = useState(null);
  const [projectFilter, setProjectFilter] = useState('');
  const [projectGradeFilter, setProjectGradeFilter] = useState('all');
  const [completedFilter, setCompletedFilter] = useState('');
  const [completedFlashFilter, setCompletedFlashFilter] = useState('all');
  const [dateRangeStart, setDateRangeStart] = useState('');
  const [dateRangeEnd, setDateRangeEnd] = useState('');
  const [showAddForm, setShowAddForm] = useState(false);
  const [sortBy, setSortBy] = useState('dateAdded');

  useEffect(() => {
    const saved = localStorage.getItem('mbp-boulders-v2');
    if (saved) {
      setBoulders(JSON.parse(saved));
    }
  }, []);

  useEffect(() => {
    localStorage.setItem('mbp-boulders-v2', JSON.stringify(boulders));
  }, [boulders]);

  const addBoulder = (grade) => {
    const newBoulder = {
      id: Date.now(),
      name: '',
      grade: grade,
      attempts: 0,
      completed: false,
      flash: false,
      notes: '',
      dateAdded: new Date().toISOString(),
      dateCompleted: null,
      sessions: []
    };
    setBoulders([newBoulder, ...boulders]);
    setFocusedBoulder(newBoulder.id);
    setShowAddForm(false);
  };

  const updateBoulder = (id, updates) => {
    setBoulders(boulders.map(b => 
      b.id === id ? { ...b, ...updates } : b
    ));
  };

  const addAttempts = (id, attemptsToAdd) => {
    setBoulders(boulders.map(b => {
      if (b.id === id) {
        const newAttempts = b.attempts + attemptsToAdd;
        return {
          ...b,
          attempts: newAttempts,
          sessions: [...b.sessions, {
            date: new Date().toISOString(),
            attempts: attemptsToAdd
          }]
        };
      }
      return b;
    }));
  };

  const markComplete = (id, isFlash = false) => {
    setBoulders(boulders.map(b => {
      if (b.id === id) {
        // Only count as flash if it's truly first attempt (no previous sessions)
        const isTrueFlash = isFlash && b.attempts === 0 && b.sessions.length === 0;
        const finalAttempts = isTrueFlash ? 1 : (b.attempts === 0 ? 1 : b.attempts);
        return {
          ...b,
          completed: true,
          flash: isTrueFlash,
          attempts: finalAttempts,
          dateCompleted: new Date().toISOString()
        };
      }
      return b;
    }));
  };

  const deleteBoulder = (id) => {
    setBoulders(boulders.filter(b => b.id !== id));
  };

  const getGradeColor = (grade) => {
    return MBP_GRADES.find(g => g.grade === grade);
  };

  const projects = boulders.filter(b => !b.completed);
  const completed = boulders.filter(b => b.completed);

  const getSortedProjects = (projectsToSort) => {
    return [...projectsToSort].sort((a, b) => {
      switch(sortBy) {
        case 'dateAdded':
          return new Date(b.dateAdded) - new Date(a.dateAdded);
        case 'attempts':
          return b.attempts - a.attempts;
        case 'grade':
          const gradeA = MBP_GRADES.find(g => g.grade === a.grade).value;
          const gradeB = MBP_GRADES.find(g => g.grade === b.grade).value;
          return gradeB - gradeA;
        default:
          return 0;
      }
    });
  };

  const filteredProjects = getSortedProjects(projects.filter(b => {
    const matchesSearch = !projectFilter || 
      (b.name && b.name.toLowerCase().includes(projectFilter.toLowerCase())) ||
      (b.notes && b.notes.toLowerCase().includes(projectFilter.toLowerCase()));
    const matchesGrade = projectGradeFilter === 'all' || b.grade === projectGradeFilter;
    return matchesSearch && matchesGrade;
  }));

  const filteredCompleted = completed.filter(b => {
    const matchesSearch = !completedFilter || 
      (b.name && b.name.toLowerCase().includes(completedFilter.toLowerCase())) ||
      (b.notes && b.notes.toLowerCase().includes(completedFilter.toLowerCase()));
    
    const matchesFlash = completedFlashFilter === 'all' || 
      (completedFlashFilter === 'flash' && b.flash) ||
      (completedFlashFilter === 'send' && !b.flash);
    
    if (dateRangeStart && dateRangeEnd) {
      const boulderDate = new Date(b.dateCompleted);
      const startDate = new Date(dateRangeStart);
      const endDate = new Date(dateRangeEnd);
      endDate.setHours(23, 59, 59);
      return matchesSearch && matchesFlash && boulderDate >= startDate && boulderDate <= endDate;
    }
    
    return matchesSearch && matchesFlash;
  }).sort((a, b) => new Date(b.dateCompleted) - new Date(a.dateCompleted));

  const getProgressData = () => {
    const sortedCompleted = [...completed].sort((a, b) => 
      new Date(a.dateCompleted) - new Date(b.dateCompleted)
    );

    const monthlyData = {};
    sortedCompleted.forEach(boulder => {
      const date = new Date(boulder.dateCompleted);
      const monthKey = `${date.getFullYear()}-${String(date.getMonth() + 1).padStart(2, '0')}`;
      
      if (!monthlyData[monthKey]) {
        monthlyData[monthKey] = { month: monthKey, sends: 0, flashes: 0, avgGrade: 0, totalGradeValue: 0 };
      }
      
      monthlyData[monthKey].sends++;
      if (boulder.flash) monthlyData[monthKey].flashes++;
      
      const gradeInfo = MBP_GRADES.find(g => g.grade === boulder.grade);
      monthlyData[monthKey].totalGradeValue += gradeInfo.value;
    });

    return Object.values(monthlyData).map(d => ({
      ...d,
      avgGrade: (d.totalGradeValue / d.sends).toFixed(1)
    }));
  };

  const getGradeDistribution = () => {
    return MBP_GRADES.map(({ grade, color }) => {
      const gradeCompleted = completed.filter(b => b.grade === grade);
      const flashes = gradeCompleted.filter(b => b.flash).length;
      return {
        grade,
        color,
        sends: gradeCompleted.length,
        flashes,
        avgAttempts: gradeCompleted.length > 0
          ? (gradeCompleted.reduce((sum, b) => sum + b.attempts, 0) / gradeCompleted.length).toFixed(1)
          : 0
      };
    }).filter(d => d.sends > 0);
  };

  const getFlashRate = () => {
    const totalCompleted = completed.length;
    const totalFlashes = completed.filter(b => b.flash).length;
    return [
      { name: 'Flashes', value: totalFlashes, color: '#eab308' },
      { name: 'Regular Sends', value: totalCompleted - totalFlashes, color: '#3b82f6' }
    ];
  };

  const formatDate = (isoString) => {
    return new Date(isoString).toLocaleDateString();
  };

  const getQuickStats = () => {
    const thisMonth = new Date();
    thisMonth.setDate(1);
    thisMonth.setHours(0, 0, 0, 0);
    
    const sendsThisMonth = completed.filter(b => 
      new Date(b.dateCompleted) >= thisMonth
    ).length;
    
    const totalBoulders = boulders.length;
    const completionRate = totalBoulders > 0
      ? Math.round((completed.length / totalBoulders) * 100)
      : 0;
    
    return {
      totalProjects: projects.length,
      totalSends: completed.length,
      sendsThisMonth,
      flashRate: completed.length > 0 
        ? Math.round((completed.filter(b => b.flash).length / completed.length) * 100)
        : 0,
      completionRate
    };
  };

  const stats = getQuickStats();

  return (
    <div className="min-h-screen bg-gradient-to-br from-slate-900 to-slate-800 text-white p-4 pb-8">
      <div className="max-w-6xl mx-auto">
        <header className="text-center mb-6 pt-6">
          <h1 className="text-4xl font-bold mb-2">MBP Boulder Tracker</h1>
          <p className="text-slate-400">Minneapolis Bouldering Project</p>
          
          {/* Quick stats bar */}
          <div className="grid grid-cols-2 md:grid-cols-4 gap-3 mt-6">
            <button
              onClick={() => setView('projects')}
              className="bg-slate-800/50 hover:bg-slate-700/50 rounded-lg p-3 transition text-left"
            >
              <div className="text-2xl font-bold text-blue-400">{stats.totalProjects}</div>
              <div className="text-xs text-slate-400">Active Projects</div>
            </button>
            <button
              onClick={() => {
                setView('completed');
                const today = new Date();
                const firstDay = new Date(today.getFullYear(), today.getMonth(), 1);
                setDateRangeStart(firstDay.toISOString().split('T')[0]);
                setDateRangeEnd(today.toISOString().split('T')[0]);
              }}
              className="bg-slate-800/50 hover:bg-slate-700/50 rounded-lg p-3 transition text-left"
            >
              <div className="text-2xl font-bold text-purple-400">{stats.sendsThisMonth}</div>
              <div className="text-xs text-slate-400">This Month</div>
            </button>
            <button
              onClick={() => {
                setView('completed');
                setCompletedFilter('');
                setCompletedFlashFilter('flash');
                setDateRangeStart('');
                setDateRangeEnd('');
              }}
              className="bg-slate-800/50 hover:bg-slate-700/50 rounded-lg p-3 transition text-left"
            >
              <div className="text-2xl font-bold text-yellow-400">{stats.flashRate}%</div>
              <div className="text-xs text-slate-400">Flash Rate</div>
            </button>
            <button
              onClick={() => setView('stats')}
              className="bg-slate-800/50 hover:bg-slate-700/50 rounded-lg p-3 transition text-left"
            >
              <div className="text-2xl font-bold text-cyan-400">{stats.completionRate}%</div>
              <div className="text-xs text-slate-400">Completion</div>
            </button>
          </div>
        </header>

        <div className="flex gap-2 mb-6 flex-wrap">
          <button
            onClick={() => setView('projects')}
            className={`flex-1 min-w-[120px] py-3 rounded-lg font-semibold transition ${
              view === 'projects' 
                ? 'bg-blue-600 text-white' 
                : 'bg-slate-700 text-slate-300 hover:bg-slate-600'
            }`}
          >
            Projects ({projects.length})
          </button>
          <button
            onClick={() => setView('completed')}
            className={`flex-1 min-w-[120px] py-3 rounded-lg font-semibold transition ${
              view === 'completed' 
                ? 'bg-blue-600 text-white' 
                : 'bg-slate-700 text-slate-300 hover:bg-slate-600'
            }`}
          >
            Completed ({completed.length})
          </button>
          <button
            onClick={() => setView('stats')}
            className={`flex-1 min-w-[120px] py-3 rounded-lg font-semibold transition ${
              view === 'stats' 
                ? 'bg-blue-600 text-white' 
                : 'bg-slate-700 text-slate-300 hover:bg-slate-600'
            }`}
          >
            Stats
          </button>
          <button
            onClick={() => setView('progress')}
            className={`flex-1 min-w-[120px] py-3 rounded-lg font-semibold transition ${
              view === 'progress' 
                ? 'bg-blue-600 text-white' 
                : 'bg-slate-700 text-slate-300 hover:bg-slate-600'
            }`}
          >
            Progress
          </button>
        </div>

        {view === 'projects' && (
          <div>
            {focusedBoulder ? (
              <div className="bg-slate-800 rounded-xl p-6 shadow-xl mb-6">
                <button
                  onClick={() => setFocusedBoulder(null)}
                  className="text-slate-400 hover:text-slate-300 mb-4 flex items-center gap-2"
                >
                  ← Back to all projects
                </button>
                
                {(() => {
                  const boulder = boulders.find(b => b.id === focusedBoulder);
                  if (!boulder) return null;
                  const gradeInfo = getGradeColor(boulder.grade);
                  
                  return (
                    <div className="text-center">
                      <div
                        style={{ 
                          backgroundColor: gradeInfo.color,
                          color: gradeInfo.textColor
                        }}
                        className="inline-block px-8 py-4 rounded-xl font-bold text-3xl mb-6"
                      >
                        {boulder.grade}
                      </div>
                      
                      <div className="text-6xl font-bold mb-2">
                        {boulder.attempts}
                      </div>
                      <div className="text-xl text-slate-400 mb-2">
                        attempt{boulder.attempts !== 1 ? 's' : ''}
                      </div>
                      
                      {boulder.sessions.length > 0 && (
                        <div className="text-sm text-slate-500 mb-6">
                          {boulder.sessions.length} session{boulder.sessions.length !== 1 ? 's' : ''} · Last: {formatDate(boulder.sessions[boulder.sessions.length - 1].date)}
                        </div>
                      )}
                      
                      <button
                        onClick={() => addAttempts(boulder.id, 1)}
                        className="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-8 rounded-xl text-2xl mb-4 transition transform active:scale-95"
                      >
                        +1 Attempt
                      </button>
                      
                      <div className="grid grid-cols-2 gap-4 mb-6">
                        <button
                          onClick={() => {
                            markComplete(boulder.id, false);
                            setFocusedBoulder(null);
                          }}
                          className="bg-green-600 hover:bg-green-700 px-6 py-4 rounded-xl text-lg font-semibold transition flex items-center justify-center gap-2"
                        >
                          <Check size={20} />
                          Sent!
                        </button>
                        <button
                          onClick={() => {
                            markComplete(boulder.id, true);
                            setFocusedBoulder(null);
                          }}
                          disabled={boulder.attempts > 0 || boulder.sessions.length > 0}
                          className={`px-6 py-4 rounded-xl text-lg font-semibold transition ${
                            boulder.attempts > 0 || boulder.sessions.length > 0
                              ? 'bg-slate-600 text-slate-400 cursor-not-allowed'
                              : 'bg-yellow-600 hover:bg-yellow-700'
                          }`}
                          title={boulder.attempts > 0 || boulder.sessions.length > 0 ? 'Cannot flash after attempts' : ''}
                        >
                          ⚡ Flash!
                        </button>
                      </div>
                      
                      {boulder.sessions.length > 0 && (
                        <details className="mb-6 text-left">
                          <summary className="cursor-pointer text-blue-400 hover:text-blue-300 mb-2 text-sm font-semibold">
                            View Session History
                          </summary>
                          <div className="bg-slate-700 rounded-lg p-3 space-y-2">
                            {boulder.sessions.map((session, idx) => (
                              <div key={idx} className="flex justify-between text-sm">
                                <span className="text-slate-300">{formatDate(session.date)}</span>
                                <span className="text-slate-400">
                                  +{session.attempts} attempt{session.attempts !== 1 ? 's' : ''}
                                </span>
                              </div>
                            ))}
                          </div>
                        </details>
                      )}
                      
                      <div className="mb-3">
                        <input
                          type="text"
                          value={boulder.name}
                          onChange={(e) => updateBoulder(boulder.id, { name: e.target.value })}
                          placeholder="Name (optional)"
                          className="w-full bg-slate-700 border border-slate-600 rounded-lg px-4 py-2 text-white text-center text-lg focus:border-blue-500 focus:outline-none placeholder:text-slate-500"
                        />
                      </div>
                      
                      <div className="mb-4">
                        <textarea
                          value={boulder.notes}
                          onChange={(e) => updateBoulder(boulder.id, { notes: e.target.value })}
                          placeholder="Notes: beta, location, observations..."
                          className="w-full bg-slate-700 border border-slate-600 rounded-lg px-4 py-3 text-white text-left focus:border-blue-500 focus:outline-none placeholder:text-slate-500 h-20"
                        />
                      </div>
                      
                      <button
                        onClick={() => {
                          if (confirm('Are you sure you want to delete this project?')) {
                            deleteBoulder(boulder.id);
                            setFocusedBoulder(null);
                          }
                        }}
                        className="text-red-400 hover:text-red-300 py-2 flex items-center gap-2 mx-auto"
                      >
                        <Trash2 size={16} />
                        Delete Project
                      </button>
                    </div>
                  );
                })()}
              </div>
            ) : (
              <>
                {!showAddForm ? (
                  <button
                    onClick={() => setShowAddForm(true)}
                    className="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-4 rounded-xl mb-6 transition flex items-center justify-center gap-2"
                  >
                    <Plus size={24} />
                    Add New Project
                  </button>
                ) : (
                  <div className="bg-slate-800 rounded-xl p-6 shadow-xl mb-6">
                    <div className="flex justify-between items-center mb-4">
                      <h2 className="text-xl font-bold">Select Grade</h2>
                      <button
                        onClick={() => setShowAddForm(false)}
                        className="text-slate-400 hover:text-slate-300"
                      >
                        <X size={24} />
                      </button>
                    </div>
                    
                    <div className="grid grid-cols-3 gap-2">
                      {MBP_GRADES.map(({ grade, color, textColor }) => (
                        <button
                          key={grade}
                          onClick={() => addBoulder(grade)}
                          style={{ 
                            backgroundColor: color,
                            color: textColor
                          }}
                          className="py-4 rounded-lg font-bold transition transform hover:scale-105"
                        >
                          {grade}
                        </button>
                      ))}
                    </div>
                  </div>
                )}

                {filteredProjects.length > 0 && (
                  <details className="bg-slate-800 rounded-xl mb-4">
                    <summary className="cursor-pointer p-4 text-sm font-semibold text-slate-300 hover:text-white">
                      Filters & Sort
                    </summary>
                    <div className="px-4 pb-4 space-y-3">
                      <input
                        type="text"
                        placeholder="Search by name or notes..."
                        value={projectFilter}
                        onChange={(e) => setProjectFilter(e.target.value)}
                        className="w-full bg-slate-700 border border-slate-600 rounded-lg px-4 py-2 text-white focus:border-blue-500 focus:outline-none"
                      />
                      <select
                        value={projectGradeFilter}
                        onChange={(e) => setProjectGradeFilter(e.target.value)}
                        className="w-full bg-slate-700 border border-slate-600 rounded-lg px-4 py-2 text-white focus:border-blue-500 focus:outline-none"
                      >
                        <option value="all">All Grades</option>
                        {MBP_GRADES.map(({ grade }) => (
                          <option key={grade} value={grade}>{grade}</option>
                        ))}
                      </select>
                      <select
                        value={sortBy}
                        onChange={(e) => setSortBy(e.target.value)}
                        className="w-full bg-slate-700 border border-slate-600 rounded-lg px-4 py-2 text-white focus:border-blue-500 focus:outline-none"
                      >
                        <option value="dateAdded">Sort by: Date Added</option>
                        <option value="attempts">Sort by: Most Attempts</option>
                        <option value="grade">Sort by: Hardest First</option>
                      </select>
                    </div>
                  </details>
                )}

                <h2 className="text-2xl font-bold mb-4">Current Projects</h2>

                <div className="space-y-3">
                  {filteredProjects.length === 0 ? (
                    <div className="bg-slate-800 rounded-xl p-8 text-center text-slate-400">
                      {projectFilter || projectGradeFilter !== 'all' 
                        ? 'No projects match your filters.' 
                        : 'No active projects. Add one above to get started!'}
                    </div>
                  ) : (
                    filteredProjects.map(boulder => {
                      const gradeInfo = getGradeColor(boulder.grade);
                      return (
                        <div 
                          key={boulder.id} 
                          className="bg-slate-800 rounded-xl p-4 shadow-lg cursor-pointer hover:bg-slate-750 transition"
                          onClick={() => setFocusedBoulder(boulder.id)}
                        >
                          <div className="flex items-start gap-4">
                            <div
                              style={{ 
                                backgroundColor: gradeInfo.color,
                                color: gradeInfo.textColor
                              }}
                              className="px-4 py-2 rounded-lg font-bold text-lg shrink-0"
                            >
                              {boulder.grade}
                            </div>
                            
                            <div className="flex-1">
                              <div className="flex items-center gap-2 mb-2">
                                {boulder.name && (
                                  <span className="font-bold text-lg">{boulder.name}</span>
                                )}
                              </div>
                              <div className="flex items-center gap-2 mb-2">
                                <span className="font-semibold text-slate-300">
                                  {boulder.attempts} attempt{boulder.attempts !== 1 ? 's' : ''}
                                </span>
                              </div>
                              
                              {boulder.notes && (
                                <div className="text-sm text-slate-300 mb-2 line-clamp-2">{boulder.notes}</div>
                              )}
                              
                              <div className="text-xs text-slate-400">
                                Added {formatDate(boulder.dateAdded)}
                              </div>
                            </div>

                            <div className="text-slate-400 shrink-0">
                              →
                            </div>
                          </div>
                        </div>
                      );
                    })
                  )}
                </div>
              </>
            )}
          </div>
        )}

        {view === 'completed' && (
          <div className="space-y-3">
            <h2 className="text-2xl font-bold mb-4">Completed Sends</h2>
            
            {completed.length > 0 && (
              <details className="bg-slate-800 rounded-xl mb-4">
                <summary className="cursor-pointer p-4 text-sm font-semibold text-slate-300 hover:text-white">
                  Filters
                </summary>
                <div className="px-4 pb-4 space-y-3">
                  <input
                    type="text"
                    placeholder="Search by name or notes..."
                    value={completedFilter}
                    onChange={(e) => setCompletedFilter(e.target.value)}
                    className="w-full bg-slate-700 border border-slate-600 rounded-lg px-4 py-2 text-white focus:border-blue-500 focus:outline-none"
                  />
                  <select
                    value={completedFlashFilter}
                    onChange={(e) => setCompletedFlashFilter(e.target.value)}
                    className="w-full bg-slate-700 border border-slate-600 rounded-lg px-4 py-2 text-white focus:border-blue-500 focus:outline-none"
                  >
                    <option value="all">All Sends</option>
                    <option value="flash">Flashes Only</option>
                    <option value="send">Regular Sends Only</option>
                  </select>
                  <div className="grid grid-cols-2 gap-3">
                    <input
                      type="date"
                      value={dateRangeStart}
                      onChange={(e) => setDateRangeStart(e.target.value)}
                      placeholder="From date"
                      className="w-full bg-slate-700 border border-slate-600 rounded-lg px-4 py-2 text-white focus:border-blue-500 focus:outline-none"
                    />
                    <input
                      type="date"
                      value={dateRangeEnd}
                      onChange={(e) => setDateRangeEnd(e.target.value)}
                      placeholder="To date"
                      className="w-full bg-slate-700 border border-slate-600 rounded-lg px-4 py-2 text-white focus:border-blue-500 focus:outline-none"
                    />
                  </div>
                  {(dateRangeStart || dateRangeEnd || completedFilter || completedFlashFilter !== 'all') && (
                    <button
                      onClick={() => {
                        setDateRangeStart('');
                        setDateRangeEnd('');
                        setCompletedFilter('');
                        setCompletedFlashFilter('all');
                      }}
                      className="text-sm text-blue-400 hover:text-blue-300"
                    >
                      Clear all filters
                    </button>
                  )}
                </div>
              </details>
            )}
            
            {filteredCompleted.length === 0 ? (
              <div className="bg-slate-800 rounded-xl p-8 text-center text-slate-400">
                {completedFilter || dateRangeStart || dateRangeEnd || completedFlashFilter !== 'all'
                  ? 'No completed sends match your filters.'
                  : 'No completed sends yet. Keep crushing!'}
              </div>
            ) : (
              filteredCompleted.map(boulder => {
                const gradeInfo = getGradeColor(boulder.grade);
                return (
                  <div key={boulder.id} className="bg-slate-800 rounded-xl p-4 shadow-lg">
                    <div className="flex items-center justify-between">
                      <div className="flex items-center gap-4 flex-1">
                        <div
                          style={{ 
                            backgroundColor: gradeInfo.color,
                            color: gradeInfo.textColor
                          }}
                          className="px-4 py-2 rounded-lg font-bold text-lg"
                        >
                          {boulder.grade}
                        </div>
                        <div className="flex-1">
                          <div className="font-semibold flex items-center gap-2 flex-wrap">
                            {boulder.name && <span className="text-lg">{boulder.name}</span>}
                            {boulder.name && <span className="text-slate-400">·</span>}
                            <span className={boulder.flash ? 'text-yellow-400' : 'text-green-400'}>
                              {boulder.flash ? '⚡ Flash!' : `✓ ${boulder.attempts} attempt${boulder.attempts !== 1 ? 's' : ''}`}
                            </span>
                          </div>
                          <div className="text-sm text-slate-400">
                            {formatDate(boulder.dateCompleted)}
                          </div>
                          {boulder.notes && (
                            <div className="text-sm text-slate-300 mt-1">{boulder.notes}</div>
                          )}
                        </div>
                      </div>
                      <button
                        onClick={(e) => {
                          e.stopPropagation();
                          if (confirm('Are you sure you want to delete this send?')) {
                            deleteBoulder(boulder.id);
                          }
                        }}
                        className="text-red-400 hover:text-red-300 p-2"
                      >
                        <Trash2 size={20} />
                      </button>
                    </div>
                  </div>
                );
              })
            )}
          </div>
        )}

        {view === 'stats' && (
          <div>
            <h2 className="text-2xl font-bold mb-6 flex items-center gap-2">
              <TrendingUp size={24} />
              Statistics
            </h2>
            
            {completed.length === 0 ? (
              <div className="bg-slate-800 rounded-xl p-8 text-center text-slate-400">
                No completed sends yet. Complete some projects to see stats!
              </div>
            ) : (
              <div className="space-y-6">
                <div className="grid grid-cols-2 gap-4">
                  <div className="bg-slate-800 rounded-xl p-6 text-center">
                    <div className="text-4xl font-bold text-blue-400">{completed.length}</div>
                    <div className="text-slate-400 mt-2">Total Sends</div>
                  </div>
                  <div className="bg-slate-800 rounded-xl p-6 text-center">
                    <div className="text-4xl font-bold text-yellow-400">
                      {completed.filter(b => b.flash).length}
                    </div>
                    <div className="text-slate-400 mt-2">Flashes</div>
                  </div>
                </div>

                <div className="bg-slate-800 rounded-xl p-6">
                  <h3 className="text-xl font-bold mb-4">Flash Rate</h3>
                  <ResponsiveContainer width="100%" height={300}>
                    <PieChart>
                      <Pie
                        data={getFlashRate()}
                        cx="50%"
                        cy="50%"
                        labelLine={false}
                        label={({ name, percent }) => `${name}: ${(percent * 100).toFixed(0)}%`}
                        outerRadius={100}
                        fill="#8884d8"
                        dataKey="value"
                      >
                        {getFlashRate().map((entry, index) => (
                          <Cell key={`cell-${index}`} fill={entry.color} />
                        ))}
                      </Pie>
                      <Tooltip 
                        contentStyle={{ backgroundColor: '#1e293b', border: '1px solid #475569' }}
                      />
                    </PieChart>
                  </ResponsiveContainer>
                </div>

                <div className="bg-slate-800 rounded-xl p-6">
                  <h3 className="text-xl font-bold mb-4">Distribution by Grade</h3>
                  <ResponsiveContainer width="100%" height={300}>
                    <PieChart>
                      <Pie
                        data={getGradeDistribution()}
                        cx="50%"
                        cy="50%"
                        labelLine={false}
                        label={({ grade, sends }) => `${grade}: ${sends}`}
                        outerRadius={100}
                        fill="#8884d8"
                        dataKey="sends"
                      >
                        {getGradeDistribution().map((entry, index) => (
                          <Cell key={`cell-${index}`} fill={entry.color} />
                        ))}
                      </Pie>
                      <Tooltip 
                        contentStyle={{ backgroundColor: '#1e293b', border: '1px solid #475569' }}
                      />
                    </PieChart>
                  </ResponsiveContainer>
                </div>

                <div className="bg-slate-800 rounded-xl p-6">
                  <h3 className="text-xl font-bold mb-4">Average Attempts by Grade</h3>
                  <ResponsiveContainer width="100%" height={300}>
                    <BarChart data={getGradeDistribution()}>
                      <CartesianGrid strokeDasharray="3 3" stroke="#475569" />
                      <XAxis dataKey="grade" stroke="#94a3b8" />
                      <YAxis stroke="#94a3b8" />
                      <Tooltip 
                        contentStyle={{ backgroundColor: '#1e293b', border: '1px solid #475569' }}
                        labelStyle={{ color: '#f1f5f9' }}
                      />
                      <Bar dataKey="avgAttempts" fill="#f59e0b" name="Avg Attempts" />
                    </BarChart>
                  </ResponsiveContainer>
                </div>

                <div className="bg-slate-800 rounded-xl p-6">
                  <h3 className="text-xl font-bold mb-4">Detailed Statistics by Grade</h3>
                  <div className="grid gap-3">
                    {getGradeDistribution().map(stat => {
                      const gradeInfo = getGradeColor(stat.grade);
                      return (
                        <div key={stat.grade} className="bg-slate-700 rounded-xl p-4">
                          <div className="flex items-center gap-4">
                            <div
                              style={{ 
                                backgroundColor: gradeInfo.color,
                                color: gradeInfo.textColor
                              }}
                              className="px-4 py-2 rounded-lg font-bold text-lg"
                            >
                              {stat.grade}
                            </div>
                            <div className="flex-1 grid grid-cols-3 gap-4 text-sm">
                              <div>
                                <div className="text-slate-400">Total Sends</div>
                                <div className="font-bold text-lg">{stat.sends}</div>
                              </div>
                              <div>
                                <div className="text-slate-400">Flashes</div>
                                <div className="font-bold text-lg">{stat.flashes}</div>
                              </div>
                              <div>
                                <div className="text-slate-400">Avg Attempts</div>
                                <div className="font-bold text-lg">{stat.avgAttempts}</div>
                              </div>
                            </div>
                          </div>
                        </div>
                      );
                    })}
                  </div>
                </div>
              </div>
            )}
          </div>
        )}

        {view === 'progress' && (
          <div className="space-y-6">
            <h2 className="text-2xl font-bold mb-4">Progress Over Time</h2>
            
            {completed.length === 0 ? (
              <div className="bg-slate-800 rounded-xl p-8 text-center text-slate-400">
                Complete some boulders to see your progress visualized!
              </div>
            ) : (
              <>
                <div className="bg-slate-800 rounded-xl p-6">
                  <h3 className="text-xl font-bold mb-4">Monthly Sends</h3>
                  <ResponsiveContainer width="100%" height={300}>
                    <BarChart data={getProgressData()}>
                      <CartesianGrid strokeDasharray="3 3" stroke="#475569" />
                      <XAxis dataKey="month" stroke="#94a3b8" />
                      <YAxis stroke="#94a3b8" />
                      <Tooltip 
                        contentStyle={{ backgroundColor: '#1e293b', border: '1px solid #475569' }}
                        labelStyle={{ color: '#f1f5f9' }}
                      />
                      <Legend />
                      <Bar dataKey="sends" fill="#3b82f6" name="Total Sends" />
                      <Bar dataKey="flashes" fill="#eab308" name="Flashes" />
                    </BarChart>
                  </ResponsiveContainer>
                </div>

                <div className="bg-slate-800 rounded-xl p-6">
                  <h3 className="text-xl font-bold mb-4">Average Grade Over Time</h3>
                  <ResponsiveContainer width="100%" height={300}>
                    <LineChart data={getProgressData()}>
                      <CartesianGrid strokeDasharray="3 3" stroke="#475569" />
                      <XAxis dataKey="month" stroke="#94a3b8" />
                      <YAxis stroke="#94a3b8" domain={[0, 10]} />
                      <Tooltip 
                        contentStyle={{ backgroundColor: '#1e293b', border: '1px solid #475569' }}
                        labelStyle={{ color: '#f1f5f9' }}
                      />
                      <Legend />
                      <Line 
                        type="monotone" 
                        dataKey="avgGrade" 
                        stroke="#10b981" 
                        strokeWidth={3}
                        name="Average Grade (V-scale)"
                      />
                    </LineChart>
                  </ResponsiveContainer>
                </div>

                <div className="bg-slate-800 rounded-xl p-6">
                  <h3 className="text-xl font-bold mb-4">Sends by Grade</h3>
                  <ResponsiveContainer width="100%" height={300}>
                    <BarChart data={getGradeDistribution()}>
                      <CartesianGrid strokeDasharray="3 3" stroke="#475569" />
                      <XAxis dataKey="grade" stroke="#94a3b8" />
                      <YAxis stroke="#94a3b8" />
                      <Tooltip 
                        contentStyle={{ backgroundColor: '#1e293b', border: '1px solid #475569' }}
                        labelStyle={{ color: '#f1f5f9' }}
                      />
                      <Legend />
                      <Bar dataKey="sends" fill="#8b5cf6" name="Total Sends" />
                      <Bar dataKey="flashes" fill="#eab308" name="Flashes" />
                    </BarChart>
                  </ResponsiveContainer>
                </div>
              </>
            )}
          </div>
        )}
      </div>
    </div>
  );
}
